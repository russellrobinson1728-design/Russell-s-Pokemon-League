# Russ’s Pokémon League — Final Retro Build

A pixel-styled life RPG inspired by early Pokémon DS-era UI conventions.

## Features
- Simultaneous badge progression
- Six evolving Pokémon: Eevee→Umbreon, Zorua→Zoroark, Sneasel→Weavile, Deino→Zweilous→Hydreigon, Gible→Gabite→Garchomp, Pawniard→Bisharp→Kingambit
- Unlimited editable monthly objectives with daily checkboxes
- Rewards, inventory, trainer card and Coat of Arms
- Supabase PC↔phone cloud save
- Controlled Push/Pull sync so connection setup cannot silently overwrite your cloud save
- Supabase `sb_publishable_...` keys supported

## Deploy
Upload all files to the root of the GitHub Pages repository and wait for the Pages deployment.

## Supabase
Use the Project URL without `/rest/v1/`. Use the publishable/anon key, never a secret/service-role key. The existing `trainer_saves` table/policies can be reused.

First-time sync: on the device with the correct save, Save Connection → Push Local Save. On the other device, Save Connection → Pull Cloud Save.
