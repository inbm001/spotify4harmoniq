# data

Spotify Liked 곡의 Ultimate Guitar 코드 수집 결과입니다. 최종 푸시는 2026-09-30 15:46 KST, 커밋 `2f5a8d3` 입니다. 이 이후 새 수집은 없습니다.

Liked 전체는 3,685곡입니다. 이 저장소에 코드 레코드로 들어 있는 곡은 파일럿 50 + 크롤 3,633 = 3,683곡입니다. Queen 「Spread Your Wings」 리마스터 Spotify 곡 2개는 크롤에서 빼고, 수동 파일 1개로 따로 두었습니다. 그 수동 파일에는 `spotify_id`가 없습니다.

## 파일

- `pilot50_results_v3.jsonl` — 파일럿 50곡. Liked 3,685곡에서 시드 42로 무작위 추출. 샤드와 겹치지 않습니다.
- `crawl_shards/shard_1.jsonl`, `shard_2.jsonl`, `shard_3.jsonl` — 나머지 3,633곡. 각 1,211줄. 줄순서는 수집 순서이고, 아티스트 순서가 아닙니다.
- `manual_spread_your_wings.json` — Queen, Spread Your Wings. 매칭 verified, 탭 v2, 키 D, 카포 없음.
- `status.json` — 마지막 푸시 시점의 줄 수. 코드 본문이 아닙니다.

파일럿과 샤드를 함치면 전체입니다. 샤드끼리 겹치지 않습니다.

## 한 줄의 형식

JSONL은 한 줄에 JSON 하나입니다.

- `spotify_id`, `title`, `artists`
- `match_status`: `verified` | `uncertain` | `mismatch`
- `parse_status`: `ok` | `partial` | `failed` | `skipped`
- `source`: Ultimate Guitar 제목, 아티스트, url, version, tab_id, type
- `parts`: `{name, chords_raw, chords_norm}` 배열. 순서와 반복을 그대로 두었습니다. `chords_raw`가 원문이고 `chords_norm`은 같은 순서의 정규화입니다.
- `key`, `capo`, `tuning`: 소스에 적힌 값만. 없으면 null.
- `collected_at`, `parser_version`, `content_hash`

쓰려도 되는 것은 `match_status`가 `verified`이고 `parse_status`가 `ok` 또는 `partial`인 줄만입니다. mismatch는 코드가 파싱되어도 성공이 아닙니다.

크롤 3,633곡만 보면 verified 1,885, uncertain 738, mismatch 1,010입니다. 파싱은 ok 2,143, partial 437, failed 43, skipped 1,010입니다. verified이면서 파싱된 곡은 1,848곡입니다.

장르는 이 파일에 없습니다. 코드는 Ultimate Guitar에서만 가져왔습니다.