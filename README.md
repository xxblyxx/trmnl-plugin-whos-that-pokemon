[![Run Tests](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/actions/workflows/test.yml/badge.svg)](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/actions/workflows/test.yml)
[![Fetch and save Pokemon](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/actions/workflows/fetch_and_save_pokemon.yml/badge.svg)](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/actions/workflows/fetch_and_save_pokemon.yml)

# trmnl-plugin-whos-that-pokemon
A TRMNL plugin that displays a different Pokémon every day using a shuffled, no-repeat rotation.

# What is it?
This repo fetches Pokémon data every day at 12:00 UTC and saves it to the repo so that it can be polled from a private plugin on TRMNL.

## No-repeat rotation
This fork changes the original fully-random selection behavior to a persistent shuffled rotation across National Pokédex IDs **1–1025**.

- All 1,025 Pokémon are shuffled into a rotation.
- One Pokémon is selected each day.
- A Pokémon will not repeat until every Pokémon in the current rotation has been shown once.
- After all 1,025 Pokémon have been used, the list is reshuffled and a new cycle begins.
- Rotation state is stored in `pokemon_data/rotation.json`, so the sequence survives between GitHub Action runs.
- The existing `pokemon_data/response.json` format is unchanged, so existing TRMNL Liquid templates continue to work.
- Manually running the workflow also advances the rotation by one Pokémon.

<img src="https://github.com/user-attachments/assets/ee7beab9-906b-49cf-9248-66ae7f270c27" alt="full" width="200"/> <img src="https://github.com/user-attachments/assets/a4460266-ec73-4901-9f78-77c5766e242d" alt="half horizontal" width="200"/> <img src="https://github.com/user-attachments/assets/3f2e1e89-01eb-4a36-80cd-2ae1e04ed920" alt="half vertical" width="200"/> <img src="https://github.com/user-attachments/assets/2ebbfa96-3029-4d5d-a074-a3221b1d9c70" alt="quadrant" width="200"/>

# How to use it?

## Recipe (easy)

The original plugin is available as a [TRMNL recipe](https://usetrmnl.com/recipes/27251/install) that can be installed with a single click. Learn more about recipes [here](https://help.usetrmnl.com/en/articles/10122094-plugin-recipes).

**Note:** The no-repeat rotation described above is specific to this fork. To use it, configure your TRMNL plugin to poll this fork's `response.json` as shown below.

## Manual install

### Step 1: Configure private plugin
1. Create a [private plugin](https://usetrmnl.com/plugin_settings?keyname=private_plugin) from the TRMNL dashboard.
2. Set the strategy to `Polling`.
3. Set the polling URL to:
   `https://raw.githubusercontent.com/xxblyxx/trmnl-plugin-whos-that-pokemon/refs/heads/main/pokemon_data/response.json`
4. Set the polling headers as `content-type=application/json`.

Refer to [settings.yml](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/blob/main/settings.yml) for more info.

### Step 2: Setup templates
Copy the full, half horizontal, half vertical and quadrant views from the `views/` directory and paste them as markup for the plugin on the dashboard.

The GitHub Action workflow [Fetch and save Pokemon](https://github.com/xxblyxx/trmnl-plugin-whos-that-pokemon/actions/workflows/fetch_and_save_pokemon.yml) runs once a day and saves the latest response in `pokemon_data/response.json`. The rotation state is saved in `pokemon_data/rotation.json`.

# Attributions
The data is obtained from [PokéAPI](https://pokeapi.co/).

This repository includes data related to Pokémon and Pokémon characters. 
© 2025 Pokémon. © 1995–2025 Nintendo/Creatures Inc./GAME FREAK inc. Pokémon and Pokémon character names are trademarks of Nintendo. All rights reserved.

The use of this data is intended for educational and non-commercial purposes only. No copyright infringements are intended. Redistribution of this repository must retain this notice along with the original licenses of any included third-party libraries. Users should be aware that the inclusion of Pokémon-related content is subject to copyright laws, and any use is at their own legal risk.

# License
This project is licensed under the Apache 2.0 License - see the [LICENSE](LICENSE) file for details.
