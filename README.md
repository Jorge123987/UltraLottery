# 🎰 UltraLotería

A configurable Minecraft lottery with ticket purchases, a growing jackpot, automatic draws, an editable inventory menu, and Vault economy support.

**Version 1.5.1** starts in Spanish and also includes English, Portuguese, and Russian language files. Server owners can edit the messages, menu, and lottery settings to fit their communities.

> The public name is **UltraLotería**. The internal plugin name remains `UltraLottery` so existing installations keep using `plugins/UltraLottery/` and their saved data.

## What does it do?

Players buy tickets using their server currency. Each ticket has an equal chance of winning. Part of every ticket sale is added to the jackpot, and the plugin draws one winning ticket when the round ends. A new round then starts automatically.

If nobody buys a ticket, the draw is postponed. If a winner is offline, their prize remains available through `/lottery claim`.

## Features

- **Ticket purchases** with a configurable price and per-player limit.
- **Dynamic jackpot** based on ticket sales; there is no fixed prize.
- **Automatic, repeating draws** with a configurable interval.
- **Configurable pot share and winner tax.**
- **Editable six-row inventory menu** with information, purchase buttons, statistics, history, and prize claiming.
- **Editable messages and announcements.**
- **Four language files:** Spanish, English, Portuguese, and Russian.
- **Optional player language selection.**
- **Winning odds, personal statistics, and recent draw history.**
- **Admin commands** to inspect, pause, resume, trigger, and manage draws.
- **Vault economy integration.**

## Requirements

- A compatible Minecraft plugin server, such as **Paper** or a compatible derivative.
- **Vault**.
- An economy plugin that registers a provider with Vault.

**Build target:** Paper API 1.20.4 and Java 17 bytecode. The JAR declares `api-version: 1.20`. Check each published release for the Minecraft versions and server software actually tested with that file.

**PlaceholderAPI is not integrated in version 1.5.1.** This version does not provide `%lottery_...%` placeholders.

## Installation

1. Install Vault and a Vault-compatible economy plugin.
2. Put `UltraLoteria-1.5.1.jar` in your server's `plugins/` folder.
3. Start the server.
4. Open `plugins/UltraLottery/config.yml` and adjust the settings.
5. Edit `plugins/UltraLottery/lang/es.yml` for messages and `plugins/UltraLottery/menus/es.yml` for the Spanish menu.
6. Run `/lottery admin reload` after editing the configuration. Restart the server after changing the additional menu command.

Keep **only one UltraLottery JAR** in `plugins/`.

## Default economy settings

| Setting | Default | Meaning |
| --- | ---: | --- |
| Ticket price | 200 | Cost of one ticket in your economy's currency |
| Tickets per player | 3 | Maximum held by one player during a round |
| Draw interval | 10,080 minutes | Seven days |
| Starting pot | 0 | No money is created when a round starts |
| Pot share | 0.90 | 90% of ticket sales enters the jackpot |
| Winner tax | 5% | Deducted from the jackpot before paying the winner |
| Tax destination | `burn` | Removes the deducted amount from circulation |

**Example:** If 100 players each buy three tickets, sales total 60,000. The jackpot receives 54,000, and the winner receives 51,300 after tax. The remaining 8,700 is removed from circulation with these default settings.

This is **only an example**. There is no 100-player cap and no guaranteed 51,300 prize. The payout changes with ticket sales and your configuration.

## Configuration files

| File | Purpose |
| --- | --- |
| `config.yml` | Languages, price, ticket limit, draw timing, pot share, tax, announcements, prefix, and additional menu command |
| `lang/es.yml` | Spanish chat messages and announcements |
| `menus/es.yml` | Spanish menu layout, title, button text, materials, and positions |
| `lang/en.yml`, `lang/pt.yml`, `lang/ru.yml` | Additional message translations |
| `menus/en.yml`, `menus/pt.yml`, `menus/ru.yml` | Additional menu translations |
| `data.yml` | Saved lottery state, tickets, prizes, and history |

The YAML files contain comments explaining their settings. Preserve configuration keys, indentation, technical menu actions such as `buy` and `claim`, and placeholders in braces such as `{amount}`.

Some menu text is written manually. If you change the ticket limit or draw interval in `config.yml`, also update menu phrases such as “3 tickets” or “7 days” in the relevant `menus/*.yml` files.

**Back up `data.yml` only while the server is stopped.** Do not delete it during an update.

## Player commands

| Command | Description |
| --- | --- |
| `/lottery` | Open the lottery menu |
| `/loteria`, `/lotto` | Aliases for `/lottery` |
| `/sorteo` | Additional menu command enabled by default; configurable |
| `/lottery buy <amount>` | Buy tickets |
| `/lottery tickets` | Check your tickets |
| `/lottery info` | Check the jackpot and next draw |
| `/lottery odds` | View your chance of winning |
| `/lottery stats` | View personal statistics |
| `/lottery history [page]` | View recent winning draws |
| `/lottery claim` | Collect a pending prize |
| `/lottery lang <en\|es\|pt\|ru>` | Choose a language if the server enables player choice |

## Administration

Administrators need the **`ultralottery.admin`** permission. It is granted to operators by default.

| Command | Description |
| --- | --- |
| `/lottery admin status` | Check lottery and pending-operation status |
| `/lottery admin draw` | Trigger a draw when tickets exist |
| `/lottery admin pause` | Pause the lottery |
| `/lottery admin resume` | Resume it |
| `/lottery admin reload` | Reload the configuration, messages, and menus |
| `/lottery admin resolve <paid\|unpaid>` | Manually reconcile a pending payout |
| `/lottery admin clearpurchase` | Clear a pending purchase after manual reconciliation |

**Check your economy's transaction records before using reconciliation commands.** Marking an operation incorrectly could cause a missing or duplicate payment.

Player commands do **not** use a `lottery.use` permission in this version.

## Updating from an earlier version

1. Stop the server.
2. Back up `plugins/UltraLottery/data.yml` and your customized YAML files.
3. Remove the previous UltraLottery JAR.
4. Add the new JAR and start the server.
5. Compare your existing configuration with the new defaults if you want newly documented settings. Existing files are not automatically overwritten.

The internal plugin name remains `UltraLottery` to preserve the existing data folder. Changing `draw-interval-minutes` may not reschedule a draw already saved for the active round; the new interval applies when the next round starts.

## License and support

**Author:** `jorge123987`  
**License:** MIT. See [LICENSE](LICENSE) for the full terms.

If you find a bug, please include your server version, Java version, Vault version, economy plugin, steps to reproduce it, and the relevant lines from `logs/latest.log` in a GitHub issue.

To support future development and testing: [PayPal donations](https://paypal.me/JorgeAlberto1589).
