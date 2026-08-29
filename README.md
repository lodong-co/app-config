# app-config

로동 앱들이 **켤 때 읽어가는 원격 설정**. 여기 파일을 고치면 앱을 새로 배포하지 않아도 값이 바뀐다.

| 앱 | 파일 |
|---|---|
| 로동 뷰어 (안드로이드 문서뷰어) | [`lodong-viewer/banner.json`](lodong-viewer/banner.json) |

## 규칙

- **공개 저장소다.** 비밀번호·키·내부 주소는 절대 넣지 말 것. 여기 들어가는 건 화면에 그대로 보이는 값뿐이다.
- 올리기 전에 JSON 문법을 확인할 것. 깨진 파일은 앱이 조용히 무시하고 이전 값을 유지한다.

```bash
python -m json.tool lodong-viewer/banner.json
```

- 앱은 켤 때 확인하고, `refreshHours`(기본 6시간)가 지났을 때만 다시 받는다. 급하면 값을 1로 낮췄다가 되돌린다.
- 서버가 죽어도, 인터넷이 안 돼도 앱은 마지막으로 받은 값(없으면 앱 내장 기본값)으로 정상 동작한다.

## 읽어가는 주소

```
https://raw.githubusercontent.com/lodong-co/app-config/main/lodong-viewer/banner.json
```

앱은 이 주소가 죽으면 `https://egghosting.com/app/lodong-viewer/banner.json` 를 대신 본다.
아예 다른 곳으로 옮기려면 설정에 `"configUrl": "https://새주소/banner.json"` 을 넣으면
앱이 다음부터 그쪽을 먼저 본다(앱 배포 불필요). 새 주소가 죽으면 자동으로 위 두 곳으로 돌아온다.
