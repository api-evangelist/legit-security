---
title: "GitHub Locks Down npm: What the New Install Defaults Mean for Your Supply Chain"
url: "https://www.legitsecurity.com/blog/github-locks-down-npm-what-the-new-install-defaults-mean-for-your-supply-chain"
date: "2026-06-17"
author: "Adi Dror"
feed_url: "https://www.legitsecurity.com/blog/rss.xml"
---
In July 2026, GitHub is going to change how npm install works for the first time in npm's history - and it's going to break some builds on purpose. Starting with npm v12 , the package manager will stop automatically running install scripts, pulling Git dependencies, or fetching dependencies from remote URLs unless you explicitly approve each one. Behavior that's been on-by-default for over a decade is becoming opt-in.
