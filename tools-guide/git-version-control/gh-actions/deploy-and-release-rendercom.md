Here’s a **GitHub Actions workflow** that automates creating a new GitHub release **after a successful deployment** to Render.com for a frontend app.

---

## **How It Works:**
1. **Deploy to Render** on `push` to the `main` branch.
2. **Wait for deployment success** using Render's API.
3. **Create a new GitHub release** with a version tag (`vX.X.X`).

---

### **1️⃣ Create GitHub Secret Variables**
You'll need to **store API tokens** securely in **GitHub Secrets**:
- **`RENDER_SERVICE_ID`** → Your Render service ID.
- **`RENDER_API_KEY`** → Your Render API key.
- **`GH_TOKEN`** → GitHub token (auto-generated, but `secrets.GITHUB_TOKEN` works for basic actions).

---

### **2️⃣ GitHub Actions Workflow**
Create `.github/workflows/deploy-and-release.yml` in your repo:

```yaml
name: Deploy to Render & Create Release

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Trigger Render Deployment
        run: |
          curl -X POST "https://api.render.com/v1/services/${{ secrets.RENDER_SERVICE_ID }}/deploys" \
               -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
               -H "Content-Type: application/json"

      - name: Wait for Deployment Success
        run: |
          while true; do
            STATUS=$(curl -s -X GET "https://api.render.com/v1/services/${{ secrets.RENDER_SERVICE_ID }}/deploys" \
              -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" | jq -r '.[0].status')
            
            echo "Deployment Status: $STATUS"

            if [[ "$STATUS" == "live" ]]; then
              echo "Deployment successful!"
              break
            elif [[ "$STATUS" == "failed" ]]; then
              echo "Deployment failed!"
              exit 1
            fi

            sleep 20
          done

  release:
    needs: deploy
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Generate Release Tag
        id: version
        run: |
          VERSION="v1.0.$(date +%s)" # Generates a version like v1.0.1708781222
          echo "VERSION=$VERSION" >> $GITHUB_ENV
          echo "Generated Version: $VERSION"

      - name: Create GitHub Release
        uses: softprops/action-gh-release@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          tag_name: ${{ env.VERSION }}
          name: "Release ${{ env.VERSION }}"
          body: "🚀 New deployment on Render is now live!"
          draft: false
          prerelease: false
```

---

## **3️⃣ How This Works**
✅ **Triggers on push to `main`**  
✅ **Deploys to Render using API**  
✅ **Waits for deployment to complete**  
✅ **If deployment is successful, creates a new GitHub release**  
✅ **Uses a timestamp-based versioning system (`v1.0.XXXXXX`)**  

---

## **4️⃣ Requirements**
- **Render API Key & Service ID:**  
  - Get them from Render → Dashboard → API → Generate Key.
  - Find Service ID from Render **Service Settings**.
- **GitHub Secrets:**  
  - Go to **GitHub → Repo → Settings → Secrets** and add:
    - `RENDER_SERVICE_ID`
    - `RENDER_API_KEY`
    - (Optional) `GH_TOKEN` if using a custom token.

---

## **5️⃣ Optional Enhancements**
- **Use Semantic Versioning:**  
  Replace `v1.0.$(date +%s)` with a dynamic versioning method.
- **Send Slack/Discord Notification** after deployment.
- **Run Tests Before Deployment:**  
  Add a step to run `npm test` before triggering Render.

---

Would you like to integrate auto-versioning (e.g., `v1.0.1`, `v1.0.2`) based on commits? 🚀
