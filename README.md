# GAP - Ghost Anchor Persistence

A fileless persistence technique affecting all Chromium-based browsers (Edge, Chrome, Brave, Vivaldi).

GAP exploits an architectural decoupling between three independent components of Chromium's extension runtime — the **Secure Preferences** file, the **Service Worker Registration database**, and the **ScriptCache** — to achieve persistent, arbitrary JavaScript execution within the browser with no malicious artifact remaining on the filesystem.

```
Secure Preferences    Extension ID -> folder B (benign, on disk)
                                   |
                          existence check only
                                   |
Service Worker DB      Registration of A (version_id unchanged)
                                   |
                            cache key lookup
                                   |
ScriptCache            Compiled background.js of A [EXECUTING]
```

## Requirements

- Initial foothold on the target machine (standard user rights sufficient)
- Target's SID value (`whoami /user`)
- [stomp](https://github.com/Fir3n0x/stomp) for extension injection and GPO bypass

## Tested Environments

| OS | Config | Post-reboot | Post-update |
|---|---|---|---|
| Windows 11 | AD + GPO | ✓ | ✓ |
| Windows 11 | Personal + GPO | ✓ | ✓ |
| Windows 11 | Personal | ✓ | ✓ |
| Windows 10 | Personal | ✓ | ✓ |

## Disclosure

Submitted to Microsoft MSRC on April 2, 2026 — Case **#112111**.  
Microsoft assessed the technique as not meeting their bar for a security update.

## Paper & Write-up

Full paper and PoC demo available respectively at **[github.com/Fir3n0x/GAP](https://github.com/Fir3n0x/GAP)** and **[fir3n0x.github.io]([https://fir3n0x.github.io](https://fir3n0x.github.io/posts/GAP-Ghost-Anchor-Persistence-Fileless-Extension-Persistence-in-Chromium-Browsers/)**.

---

*Corentin Mahieu — [fir3n0x.github.io](https://fir3n0x.github.io)*
