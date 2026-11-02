# IR recipes for LightCraft's channel mixer

Fifteen presets for playing with infrared photos in [LightCraft](https://github.com/storytold/lightcraft), using the
RGB channel mixer proposed in [storytold/lightcraft#3579](https://github.com/storytold/lightcraft/pull/3579). They're for
experimenting: some look good, some look wild, a few look silly on purpose.

**Not official, not part of LightCraft,** and they only work in a build of that pull request (see below). They were
tuned on one camera: a Sony A6000 converted with a 590 nm filter.

![The fifteen recipes on one 590 nm photo of Mt. Hood](contact-sheet.jpg)

## Getting a build with the mixer

The mixer isn't in a LightCraft release yet. To try it, build the pull request's branch (you need [Rust](https://rustup.rs)):

```bash
git clone --branch feat/channel-mixer https://github.com/darthnut/lightcraft.git lightcraft-mixer
```

```bash
cd lightcraft-mixer
```

```bash
cargo run --release -p lightcraft -- --library ~/lightcraft-mixer-test
```

The `--library` folder keeps this test build away from your real LightCraft library. LightCraft's own README covers
build requirements and low-memory build settings.

## Install the recipes

Download [`IR Recipes.lcpreset`](IR%20Recipes.lcpreset). In the Presets panel, click **Import Presets…** and choose it.
They appear in three groups: **IR Recipes 1 · Classic**, **2 · Wild** and **3 · Silly**.

## Use one

1. Click a recipe.
2. If its name says **(pick …)**, click the Channel Mixer's neutral picker and click on what it names:
   - **snow/cloud/concrete:** anything that should be white or grey.
   - **foliage:** bright leafy trees or grass.

   The picker fits the recipe to your photo. Skipping it gives a fairly random colour cast.
3. Set Exposure, Highlights and Shadows to taste. The recipes don't touch them, except Day for Night.

**Switching recipes:** apply the new recipe, then pick again. A recipe resets the mixer.

**White balance jumps to 2000 K:** the picked recipes set it on purpose. A 590 nm raw is so red that some mixers black
out the spot before the picker can measure it, and it refuses ("pick a brighter, less saturated area"). The pick
cancels white balance anyway, so this doesn't change the colours.

## The recipes

| Recipe | Pick | Look |
| --- | --- | --- |
| Classic Swap | neutral | The textbook red/blue swap. On a 590 nm filter that gives pink foliage and a teal sky |
| Hood River Pink | neutral | The colour settings of the Mt. Hood edit in the pull request |
| White Foliage, Blue Sky | foliage | White trees under a blue sky |
| Gold Foliage, Blue Sky | neutral | Gold trees, the look many 590 nm tutorials show |
| Soft Pastel | neutral | Half swap, low contrast, a faint pink/teal split tone |
| IR Mono, Wood Effect | none | Black and white from the red channel, punchy |
| IR Mono, Soft Glow | none | Same source, negative Clarity for a dreamy glow |
| Faux Aerochrome | neutral | Red foliage in the style of Kodak Aerochrome film |
| Fake Summer | neutral | Green trees again, though not quite the right green |
| Teal Forest, Orange Sky | neutral | Complementary teal and orange |
| Lava Fields | neutral | Brick-red land under a violet sky |
| Alien Planet | neutral | Magenta trees, a green-tinted sky |
| Night Vision Goggles | none | Green phosphor, vignette and grain; lower Exposure if it's too bright |
| Day for Night | neutral | Old-Hollywood fake moonlight: dark, blue, desaturated |
| Mars Holiday | foliage | Everything rust and dust |

## How they were made

- **Measured, not guessed.** Tutorials disagree about what a 590 nm red/blue swap gives (gold foliage or pink). On this
  camera it's pink. So the colours of snow, foliage and sky were measured in a real raw. Each "wild" mixer was solved
  to send those colours to a target hue, then checked by rendering it.
- **Always pickable.** In every picked recipe, each mixer row adds up to 100 %. That guarantees the neutral picker can
  solve it.
- **One camera, one scene.** Other filters (665, 720 nm…), cameras and subjects will land differently. That's the
  experiment: if you find better numbers for your setup, please share them.

`make_recipes.py` regenerates the preset file. Edit the numbers, run `python make_recipes.py`, then delete the old
presets in LightCraft before importing again: importing doesn't replace a preset with the same id.

Made by darthnut with Claude (Anthropic). Licensed MIT or Apache-2.0, like LightCraft.
