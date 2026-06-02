---
license: other
language:
- en
pretty_name: Stravl Travel Preference Dataset
size_categories:
- 10K<n<100K
task_categories:
- tabular-classification
tags:
- travel
- recommendation
- preferences
- tabular
- user-behavior
dataset_info:
  features:
  - name: id
    dtype: string
  - name: form_a
    dtype: string
  - name: form_a_age_ranges
    sequence: string
  - name: form_b
    dtype: string
  - name: form_b_trip_budget
    sequence: string
  - name: form_c
    dtype: string
  - name: form_c_travel_season
    sequence: string
  - name: form_f
    dtype: string
  - name: form_f_experiences
    sequence: string
  - name: form_g
    dtype: string
  - name: form_g_scenery
    sequence: string
  - name: form_h
    dtype: string
  - name: form_h_activity_level
    sequence: string
  - name: form_i
    dtype: string
  - name: form_i_safety_conscious
    sequence: string
  - name: form_j
    dtype: string
  - name: form_j_destination_popularity
    sequence: string
  - name: form_k
    dtype: string
  - name: form_r
    dtype: string
  - name: form_r_destination_choice
    sequence: string
  - name: form_rr
    dtype: string
  - name: form_rr_specific_regions
    sequence: string
  - name: yes_swipes
    dtype: string
  - name: yes_swipes_names
    sequence: string
  - name: no_swipes
    dtype: string
  - name: no_swipes_names
    sequence: string
  - name: maybe_swipes
    dtype: string
  - name: maybe_swipes_names
    sequence: string
  - name: Model
    dtype: int64
  - name: Retrieval
    dtype: int64
  - name: DynaMatch
    dtype: int64
  splits:
  - name: train
    num_examples: 80301
configs:
- config_name: default
  data_files:
  - split: train
    path: data/train-*
---

*Source data from the [Stravl/Stravl-Data](https://github.com/Stravl/Stravl-Data) GitHub repository. This dataset is a derived, HuggingFace-ready version with human-readable label columns added.*

# Stravl Travel Preference Dataset

Stravl-Data is one of the world's largest open-sourced datasets of travel preferences. Through a user-facing website, Stravl gathered **80,301 travelers' vacation preferences**. Users were asked to fill out a brief form on their ideal vacation (such as expected experiences, scenery, and activity level) and logistical constraints (such as budget, traveler ages, and season). Thereafter, they "swiped" or "rated" ten destinations, responding with "Yes", "No", or "Maybe" in a Tinder-like rating framework. In total, **over 1,000,000 user swipes** were recorded. Lastly, users were shown 5 to 10 recommendations selected by different ML models; those recommendations and the users' feedback on them are stored.

Personally-identifying information such as IP data, user names, or other metadata has been removed prior to release.

## What's different in this version

This version is derived from the [original GitHub dataset](https://github.com/Stravl/Stravl-Data) for convenient use with the 🤗 `datasets` library. On top of the original columns, **human-readable label columns** have been added directly beside their coded counterparts:

- Each form column (`form_a` … `form_rr`) gets a descriptive sequence column resolving its codes to labels (e.g. `form_b` → `form_b_trip_budget`).
- Each swipe column (`yes_swipes`, `no_swipes`, `maybe_swipes`) gets a `*_names` column resolving destination indices to destination names.

The original coded columns are preserved unchanged.

## Dataset Structure

| Column | Type | Description |
|--------|------|-------------|
| **id** | string | Anonymized user identifier |
| **form_a** … **form_rr** | string | Raw form responses, each a stringified list of codes (e.g. `"['0', '1']"`) |
| **form_a_age_ranges** | sequence[string] | Decoded labels for `form_a` (travel group age ranges) |
| **form_b_trip_budget** | sequence[string] | Decoded labels for `form_b` (budget per person, per night) |
| **form_c_travel_season** | sequence[string] | Decoded labels for `form_c` (season) |
| **form_f_experiences** | sequence[string] | Decoded labels for `form_f` (desired experiences) |
| **form_g_scenery** | sequence[string] | Decoded labels for `form_g` (desired scenery) |
| **form_h_activity_level** | sequence[string] | Decoded labels for `form_h` (activity level) |
| **form_i_safety_conscious** | sequence[string] | Decoded labels for `form_i` (safety preference) |
| **form_j_destination_popularity** | sequence[string] | Decoded labels for `form_j` (destination popularity) |
| **form_k** | string | Raw form response (undocumented; preserved as-is, no decoded column) |
| **form_r_destination_choice** | sequence[string] | Decoded labels for `form_r` (anywhere vs. specific regions) |
| **form_rr_specific_regions** | sequence[string] | Decoded labels for `form_rr` (chosen regions) |
| **yes_swipes / no_swipes / maybe_swipes** | string | Stringified lists of destination indices the user swiped Yes / No / Maybe |
| **yes_swipes_names / no_swipes_names / maybe_swipes_names** | sequence[string] | Destination names corresponding to the swipe indices |
| **Model / Retrieval / DynaMatch** | int | Which recommendation algorithm(s) were used (`-1` = not tracked) |
| **Rating_0** … **Rating_9** | int | User feedback per recommendation: `1` = approved, `-1` = disapproved, empty = not rated. All `-1` = ratings not tracked for this user |
| **Rec_0** … **Rec_9** | string | Recommended destination names, in recommendation order (`-1` = not tracked) |

### Form Response Encodings

The decoded columns above are produced from these mappings (sourced from the original dataset documentation).

**FORM_A** — Age ranges in the travel group *(multi-select)*: `0` 0-19 · `1` 20-39 · `2` 40-59 · `3` 60+

**FORM_B** — Trip budget (per person, per night): `0` $0-$49 · `1` $50-$99 · `2` $100-$249 · `3` $300+

**FORM_C** — Travel season: `0` Winter · `1` Spring · `2` Summer · `3` Fall

**FORM_F** — Experiences sought *(multi-select)*: `0` Beach · `1` Adventure · `2` Nature · `3` Culture · `4` Nightlife · `5` History · `6` Shopping · `7` Cuisine

**FORM_G** — Scenery sought *(multi-select)*: `0` Urban · `1` Rural · `2` Sea · `3` Mountain · `4` Lake · `5` Desert · `6` Plains · `7` Jungle

**FORM_H** — Activity level: `0` Chill & Relaxed · `1` Balanced · `2` Active

**FORM_I** — Safety conscious: `0` Very Safety Conscious · `1` Balanced · `2` Ready for Anything

**FORM_J** — Destination popularity: `0` Off the Beaten Path · `1` Classic Spot · `2` Mainstream & Trendy

**FORM_R** — Where do you want to go?: `0` Anywhere · `1` Specific Regions

**FORM_RR** — Which specific regions? *(multi-select, only if `form_r` = Specific Regions)*: `e` Europe · `n` N. America · `c` Caribbean · `a` Asia · `s` S. America · `m` Mid. East · `f` Africa · `o` Oceania

> **Note:** `form_k` appears in the source data but is not documented in the original dataset. It is preserved unchanged, and no decoded column is generated for it.

### Swipe & Recommendation Responses

- **Swipes:** `yes_swipes`, `no_swipes`, and `maybe_swipes` are lists of indices into a destination table; the `*_names` columns resolve them to destination names.
- **Recommendations & Ratings:** Users were recommended 5 destinations (or 10 if they asked for more). The `Model`, `Retrieval`, and `DynaMatch` fields indicate which algorithms produced them; the algorithm implementations are not released. `Rec_*` holds the recommended destination names in order, and `Rating_*` holds user feedback on each (`1` approve, `-1` disapprove, empty = unrated; all `-1` = ratings not tracked for that user).

## Dataset Statistics

- **Users:** 80,301
- **Total swipes:** 1,000,000+
- **Destinations:** 1,486 unique destinations
- **Language:** English

## Usage

```python
from datasets import load_dataset

ds = load_dataset("chuuhtetnaing/stravl-travel-preference-dataset")

example = ds["train"][0]
print("Liked:", example["yes_swipes_names"])
print("Budget:", example["form_b_trip_budget"])
print("Experiences:", example["form_f_experiences"])
```

## Limitations

- Form responses are self-reported and reflect each user's stated preferences at the time of the survey.
- Recommendation algorithm implementations (`Model`, `Retrieval`, `DynaMatch`) are not released — only their selections are shared.
- Recommendations and ratings were not tracked for all users (`-1` markers indicate untracked entries).

## License

This dataset is published under permissive terms inherited from the upstream source. Per the original Stravl documentation, the data is **free to use for any academic or commercial purposes**. There is no formal LICENSE file in the source repository; for questions about usage, contact **info@stravl.com**.

## Acknowledgments

This dataset is derived from [**Stravl/Stravl-Data**](https://github.com/Stravl/Stravl-Data) on GitHub. All credit for collecting and open-sourcing the original travel preference data goes to Stravl. This HuggingFace release adds human-readable label columns for convenience and is maintained as a fork of the original repository.
