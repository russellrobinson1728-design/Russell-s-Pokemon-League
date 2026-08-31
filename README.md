# Russ's Pokémon League V4

## Included
- Six Pokémon with circular individual image frames and live evolution sprites.
- Starters: Eevee, Zorua, Sneasel, Deino, Gible, Pawniard.
- Final forms: Umbreon, Zoroark, Weavile, Hydreigon, Garchomp, Kingambit.
- All eight badges progress simultaneously.
- Monthly objectives: unlimited editable objectives with daily checkbox tracking.
- Custom quest modal resets cleanly every time and badge allocation is aligned.
- More descriptive quest/objective wording.
- Optional Supabase cloud sync for PC ↔ phone.

## GitHub Pages
Upload every file in this folder to the root of your public GitHub repository. Deploy `main` / root.

## Supabase cross-device sync
GitHub Pages cannot share browser localStorage between devices. Supabase supplies the shared cloud save.

In Supabase SQL Editor run:

```sql
create table if not exists public.trainer_saves (
  id text primary key,
  data jsonb not null,
  updated_at timestamptz not null default now()
);

alter table public.trainer_saves enable row level security;

create policy "league select" on public.trainer_saves for select to anon using (true);
create policy "league insert" on public.trainer_saves for insert to anon with check (true);
create policy "league update" on public.trainer_saves for update to anon using (true) with check (true);
```

Then copy Project URL and anon/public key from Supabase Project Settings → API.
Open the app's Sync page on PC, enter those values and Trainer ID `russ`, then Connect & Push.
Open the same app on phone, enter the same values and Trainer ID, then Pull Cloud Save once. Later edits automatically push to the cloud after a short delay.

These anonymous policies are suitable only for a personal prototype. For a public production app, use Supabase Auth and per-user row security.

## Pokémon sprites
Individual sprites are loaded at runtime from the PokeAPI sprites repository.


## V4 sync behavior
- **Save Connection** never uploads and never overwrites a cloud save.
- **Push Local Save** explicitly uploads this device's save.
- **Pull Cloud Save** explicitly replaces this device's local save with the cloud save.
- Automatic pushes only begin after a successful explicit Push or Pull.
- The app removes an accidentally pasted `/rest/v1/` suffix from the Project URL.
- First-time setup should always be: main device -> Push -> other device -> Pull.
