 name: Update Stats Card
        
        permissions:
          contents: write
        
        on:
          workflow_dispatch:
          push:
            branches:
              - main
          schedule:
            - cron: "0 8 * * *" # This will run the workflow every day 8:00 pm IST
        
        jobs:
          update-stats-card:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout repository
                uses: actions/checkout@v3
        
              - name: Fetch Stats and Save SVG
                run: |
                  # Fetch the latest stats card as an SVG
                  curl -o stats.svg https://www.dsastats.site/api/codolio/{@ZJQPagIV}
                  
              - name: Force Commit changes
                run: |
                  git config --global user.name 'github-actions[bot]'
                  git config --global user.email 'github-actions[bot]@users.noreply.github.com'
                  
                  # Add a timestamp to the commit message to ensure a new commit is created
                  git add stats.svg
                  git commit -m "Update stats card $(date +'%Y-%m-%d %H:%M:%S')"
                  
                  # Pull latest changes from remote to avoid conflicts
                  git pull --rebase
                  
                  # Push the changes to the remote repository
                  git push

<!--
**Shreytan/Shreytan** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
