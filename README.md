# TestDriver Bot Playground

# TestDriver.ai

Automate and scale QA with agentic users.

[Docs](https://docs.testdriver.ai) | [Website](https://testdriver.ai) | [GitHub Action](https://github.com/marketplace/actions/testdriver-ai) | [Join our Discord](https://discord.gg/a8Cq739VWn)

---

# Demo

Ask [@testdriverbot](https://github.com/testdriverbot) to test your app within any issue or pull request! Just tag [@testdriverbot](https://github.com/testdriverbot) and include a markdown list of tasks. You can try it right now [in this repo](https://github.com/testdriverai/bot-playground/pull/1).

![CleanShot 2024-12-10 at 15 14 54](https://github.com/user-attachments/assets/790a89dc-c96b-44e7-8ee6-b4e559a8170e)

# Overview

Tag [@testdriverbot](https://github.com/testdriverbot) in your repo and provide a markdown list of steps to take.

```sh
@testdriverbot

1. open youtube.com
2. search for rick astley
3. click the first video
4. verify the video is playing
```

TestDriver will spawn an ephemeral Windows VM with Chrome launched and attempt to complete your task. This might take a few minutes! TestDriver will make a comment and ping you when it's done.

You can click on the animated GIF to see the full test recording.

![CleanShot 2024-12-10 at 15 15 55](https://github.com/user-attachments/assets/13de34c4-440d-45c1-b67c-cf5ea3a34e0b)

# How do I turn this into a regression test?

Add the `/save` command and TestDriver will generate a YML file. Then, use [our GitHub action](https://docs.testdriver.ai/continuous-integration/github-setup) to re-run this test on every PR, commit, or merge!

```yml
- uses: testdriverai/action@main
  with:
    key: ${{ secrets.TESTDRIVER_API_KEY }}
    prompt: 1. /run testdriver/test.yml
    prerun: |
      cd $env:TEMP
      npm init -y
      npm install dashcam-chrome
      Start-Process "C:/Program Files/Google/Chrome/Application/chrome.exe" -ArgumentList "--start-maximized", "--load-extension=$(pwd)/node_modules/dashcam-chrome/build", "${{ env.WEBSITE_URL }}"
      exit
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    FORCE_COLOR: "3"
```

# Can this validate PRs?

Yes! You need to deploy to GitHub pages, Vercel preview, or upload an artifact first. Then, have TestDriver download that artifact as part of the [prerun script](https://docs.testdriver.ai/continuous-integration/prerun-scripts).

# Does this work for private repos?

Yes, just add @testdriverbot as a collaborator.
