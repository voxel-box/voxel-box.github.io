# Chat Archive — Starter Kit

This folder is a staging area for a **private** chat-archive repository.
It should be moved to a private repo (e.g. `voxel-box/chat-archive`) —
do **not** merge it into the public website, since chat logs may contain
personal or sensitive information.

## Setting up the private repo

1. Go to https://github.com/new
2. Name it `chat-archive` (or anything you like), set **Visibility: Private**,
   and check "Add a README".
3. Grant the Claude GitHub app access to the new repo
   (github.com → Settings → Applications → Claude → Repository access).
4. In a Claude session, say: *"add voxel-box/chat-archive and copy the
   starter kit from voxel-box.github.io into it"* — done.

## Repository structure

```
chat-archive/
├── README.md
└── chats/
    └── YYYY-MM-DD/            # one folder per day
        ├── <topic-slug>.md    # one file per conversation
        └── ...
```

## Getting chats into the archive

Claude sessions run in isolated containers, so past conversations can't be
read automatically. To publish a chat, use one of these:

- **Export from claude.ai**: Settings → Privacy → Export data. You'll get an
  email with a download containing all conversations as JSON. Share the file
  in a Claude session and ask to convert and publish it.
- **Paste or upload**: paste a conversation (or attach a file) into a Claude
  session and ask to publish it to the archive.
- **Going forward**: at the end of any session, ask Claude to "publish this
  chat to the archive" — it can write up the session and commit it directly.

Each published chat should follow [TEMPLATE.md](TEMPLATE.md).
