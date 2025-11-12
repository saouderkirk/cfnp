# Help! Trying to Get Started with Kixx 6.0 and Running Into Some Snags

Hey friends!

So I just discovered Kixx and honestly I'm pretty pumped about it - the whole hypermedia-driven approach is *exactly* what I've been looking for. But I'm hitting some bumps trying to get 6.0.0 running and I'm hoping someone can help me figure out what I'm missing!

## The Short Version
I'm getting errors right out of the gate with a fresh install of 6.0.0. Tried both the init and server commands, documented everything below. Not sure if I'm doing something wrong or if there's a setup step I missed?

## What's Happening

Started with the basics from the docs:
```bash
npm init -y
npm install kixx@6.0.0
npx kixx init-project --name "My App"
```

This immediately errors out looking for a `.gitignore` file that doesn't exist in the project template.

So I tried a quick workaround:
```bash
touch node_modules/kixx/project-template/.gitignore
npx kixx init-project --name "My App"  # This part works now!
npx kixx app-server --environment development
```

But now I'm getting: `"Unable to get 'app.Root' user constructor as root user"`

## What I'm Wondering

- Did I miss a setup step? Is there some plugin configuration I should be doing?
- Has anyone else gotten 6.0.0 running successfully? Would love to know what your setup looks like!
- Should I just roll back to 5.2.0 for now? (Though that one seems to have a quirk with the port config too)

## My Setup
- Node: 16.13.2+
- OS: macOS
- Fresh install, no prior Kixx projects

## Why I'm Here

Look, I'm genuinely excited about what you all are building with Kixx. The philosophy resonates hard - especially the focus on AI-friendly development and keeping things simple. I really want to dig in and start building with it!

I've got detailed notes on everything I tried, happy to share more info or help test anything. And once I get this figured out, I'd love to contribute back - whether that's docs improvements, testing, or whatever else would be helpful.

Just trying to get over this initial hump so I can actually start playing with it!

Anyone have thoughts on what might be going on? Or am I just being dense and missing something obvious? 😅

Thanks in advance - really appreciate any help! 🙏

---

**P.S.** I've got a more detailed bug report written up if that would be useful, just didn't want to dump a wall of text on you all right away!
