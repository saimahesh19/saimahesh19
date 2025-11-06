# 🐍 GitHub Contribution Snake Animation Setup Guide

## What is the Snake Animation?

The snake animation shows a snake eating your GitHub contributions! It's a cool visual effect that makes your profile stand out. The snake moves through your contribution graph, eating the green squares.

---

## 📋 Setup Instructions

### Step 1: Create a Special Repository

1. Go to GitHub and create a **new repository**
2. Name it **exactly** as your username: `saimahesh19`
3. Make it **Public**
4. Initialize with a README (you can use the GITHUB_PROFILE_README.md I created)

### Step 2: Enable GitHub Actions

1. Go to your repository settings
2. Click on **Actions** → **General**
3. Under "Workflow permissions", select **Read and write permissions**
4. Click **Save**

### Step 3: Create the Workflow File

1. In your `saimahesh19` repository, create this folder structure:
   ```
   .github/workflows/
   ```

2. Inside the `workflows` folder, create a file named `snake.yml`

3. Copy and paste this code into `snake.yml`:

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"  # Runs every 12 hours
  workflow_dispatch:  # Allows manual trigger
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: saimahesh19
          outputs: |
            /images/GitHubContributionSnake.jpg
            /images/photo1762425634.jpg

      - name: Push snake animations to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Step 4: Trigger the Workflow

1. Go to **Actions** tab in your repository
2. Click on "Generate Snake Animation" workflow
3. Click **Run workflow** → **Run workflow**
4. Wait 1-2 minutes for it to complete

### Step 5: Update Your Profile README

The snake animation is now generated! Use this URL in your README:

```markdown
![Snake animation](https://raw.githubusercontent.com/saimahesh19/saimahesh19/output/github-contribution-grid-snake-dark.svg)
```

---

## 🎨 Customization Options

### Change Colors

Edit the `snake.yml` file and modify the `palette` parameter:

```yaml
outputs: |
  /images/GitHubContributionSnake.jpg
  /images/photo1762425634.jpg
  dist/github-contribution-grid-snake-blue.svg?palette=github-blue
```

Available palettes:
- `github-light` - Light theme
- `github-dark` - Dark theme (default)
- `github-blue` - Blue theme

### Change Update Frequency

Modify the cron schedule in `snake.yml`:

```yaml
schedule:
  - cron: "0 */6 * * *"  # Every 6 hours
  - cron: "0 0 * * *"    # Daily at midnight
  - cron: "0 */12 * * *" # Every 12 hours (recommended)
```

---

## 🐛 Troubleshooting

### Snake Not Showing?

1. **Check Actions Tab**: Make sure the workflow ran successfully
2. **Check Output Branch**: Verify the `output` branch exists with SVG files
3. **Wait 5 minutes**: GitHub Pages can take a few minutes to update
4. **Clear Browser Cache**: Hard refresh (Ctrl+Shift+R or Cmd+Shift+R)

### Workflow Failing?

1. **Check Permissions**: Ensure "Read and write permissions" is enabled
2. **Check Repository Name**: Must match your username exactly
3. **Check Branch Name**: Default branch should be `main` (not `master`)

### Snake Not Moving?

The snake animation is static (SVG). It shows the path the snake took through your contributions. Make more commits to see it change!

---

## 🎯 Pro Tips

1. **Make Regular Commits**: The snake gets longer with more contributions
2. **Contribute Daily**: Creates a more interesting snake pattern
3. **Use Dark Theme**: Looks better on most GitHub profiles
4. **Pin Important Repos**: Showcase your best work alongside the snake

---

## 📚 Additional Resources

- [Platane/snk GitHub](https://github.com/Platane/snk) - Original snake generator
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Cron Expression Generator](https://crontab.guru/) - Create custom schedules

---

## ✅ Checklist

- [ ] Created repository named `saimahesh19`
- [ ] Enabled GitHub Actions with write permissions
- [ ] Created `.github/workflows/snake.yml` file
- [ ] Ran the workflow successfully
- [ ] Verified `output` branch exists
- [ ] Added snake animation to README
- [ ] Snake animation displays correctly

---

**🎉 Congratulations! Your GitHub profile now has a cool snake animation!**

**Note:** The snake updates automatically every 12 hours, or you can manually trigger it from the Actions tab.
