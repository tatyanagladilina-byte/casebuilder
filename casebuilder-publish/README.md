# casebuilder

AI-интервьюер для дизайнеров. Собери Behance-кейс за 45 минут вместо 2 дней.

## Структура

- `index.html` — главная страница лендинга
- `casebuilder-images/founder.jpeg` — фото founder секции
- `blockscout-case/` — реальный кейс Blockscout (на него ведёт ссылка из Examples)

## Развёртывание (GitHub Pages)

После загрузки файлов в репозиторий:

1. Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main`, folder: `/ (root)`
4. Save

URL появится через ~1 минуту: `https://tatyanagladilina-byte.github.io/casebuilder/`

Чтобы привязать кастомный домен (например `casebuilder.design`) — добавь его в Settings → Pages → Custom domain и пропиши CNAME у регистратора на `tatyanagladilina-byte.github.io`.

## Waitlist (Supabase)

Форма пишет email прямо в таблицу `waitlist` через REST API. Перед публикацией нужно создать таблицу:

```sql
create table waitlist (
  id uuid default gen_random_uuid() primary key,
  email text unique not null,
  created_at timestamp with time zone default now(),
  source text default 'casebuilder-landing'
);

alter table waitlist enable row level security;

create policy "anon insert"
  on waitlist for insert
  to anon
  with check (true);
```

Запусти этот SQL в Supabase → SQL Editor → New Query → Run.
