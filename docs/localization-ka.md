# FigCraft in Georgian

> **Last reviewed:** 2026-10-18 · **Last updated:** 2026-10-19 · **Change:** patch (catalog complete again after the upstream merge: missing fonts, home-screen search; previously minor: .fig import notes, selection colors, paste design layers) · **Target:** Figma Design (desktop app 126.10.7)

Choose **Preferences ▸ Language ▸ ქართული**. The interface switches at once and the choice is saved
with the other preferences. With **System**, FigCraft reads Georgian when the first of the OS's
preferred languages is Georgian (`ka`, `ka-GE`, `ka_GE.UTF-8`). `pref.language {"language": "ka"}`
selects it from the CLI, MCP and the control channel. New files and pages are named in the interface
language (`უსათაურო`, `გვერდი 1`).

`crates/ui-egui/locales/ka.toml` translates every key of `en.toml` (1,731 UI strings), every command
label (567) and every menu wording (31): menus, panels, the Actions palette, the shortcuts panel,
dialogs, tooltips, toasts, the home screen and templates. Command ids, CLI/MCP/control-channel output,
file names and the names you give layers, styles and variables stay as they are. The catalog was
written from the meaning of the English labels; no proprietary translation resources were consulted.
It is a draft waiting for native speakers' review.

## Georgian script

Mkhedruli has no upper and lower case: title case and capitalising leave it alone, and ALL CAPS
would turn it into Mtavruli (Unicode), so the interface never uppercases Georgian labels. Commands
are verbal nouns (`გვერდის დამატება`). Counts are count-neutral, noun first, so both plural forms
read the same: `შრე: {n}` (a test checks every plural entry).

Inter and egui's own fonts have no Georgian letters, and craft-fonts has no Georgian face yet
(storytold/craft-fonts#27 adds Noto Sans Georgian). Until then the desktop app adds an installed
Georgian face when something on screen needs it (`crates/ui-egui/src/cjk.rs`); the web build has
none and leaves Georgian out of the picker.

## Terminology

| Source | Georgian |
|---|---|
| File / Edit / View | ფაილი / რედაქტირება / ხედი |
| Object / Text / Arrange | ობიექტი / ტექსტი / დალაგება |
| Preferences / Language | პარამეტრები / ენა |
| Design / Prototype / Dev Mode | დიზაინი / პროტოტიპი / დეველოპერის რეჟიმი |
| Layers / Assets / Pages | შრეები / რესურსები / გვერდები |
| Frame / Group / Section | ჩარჩო / ჯგუფი / სექცია |
| Component / Instance / Variant | კომპონენტი / ინსტანსი / ვარიანტი |
| Detach instance | ინსტანსის გამოყოფა |
| Auto layout / Constraints | ავტოგანლაგება / შეზღუდვები |
| Fill / Stroke / Effects | შევსება / კონტური / ეფექტები |
| Styles / Variables / Mode | სტილები / ცვლადები / რეჟიმი |
| Mask / Boolean groups | ნიღაბი / ლოგიკური ოპერაციების ჯგუფები |
| Vector / Pen | ვექტორი / კალამი |
| Interaction / Smart animate | ურთიერთქმედება / ჭკვიანი ანიმაცია |
| Inspect / Export | ინსპექტირება / ექსპორტირება |
| Comments / Share | კომენტარები / გაზიარება |
| Libraries / Plugins | ბიბლიოთეკები / პლაგინები |
| Undo / Redo | დაბრუნება / ხელახლა შესრულება |
| Untitled / Page | უსათაურო / გვერდი |

Please follow this table and the shared ArtCraft Georgian glossary when you add strings.

## Maintenance and checks

Add a string to `ka.toml` under the same key as in `en.toml` (`[ui]`), or under its command id
(`[commands]`, `[menu]`). Keep `{placeholders}`, `…`, `\n`, brand names and keyboard glyphs exactly;
give plural entries the same text for `one` and `other` where English counts in both. A key the
catalog lacks shows in English.

```sh
cargo test -p figcraft-ui-egui i18n
```

The tests check known keys, matching placeholders, plural shape, the `ka` locale tags, the draft
status and the count-neutral plurals; `cjk.rs` tests check the Georgian script detection. More in
[translating.md](translating.md) and [localization-parity.md](localization-parity.md).
