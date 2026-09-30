## 컨벤져스에서 쓰는 법 (convengers 브랜치 안내)

코드리뷰를 여섯 단계로 자동으로 돌리는 Claude Code 플러그인입니다. 설계 의도를 쓰고, 평가 기준을 뽑고, PR 본문을 만들고, 리뷰하고, 반영까지 합니다.

1. 이 폴더의 `convengers/skills/` 아래 일곱 폴더를 키트의 `plugins/convengers/skills/` 로 복사합니다.
2. 리뷰할 프로젝트에 `plugin/docs/code-convention.yaml` 과 `plugin/docs/adr.yaml` 을 복사해 우리 팀 규칙으로 고칩니다.
3. Claude Code에서 `/convengers:mafia-codereview-auto` 를 칩니다. 산출물은 `.review-artifacts/브랜치이름/` 에 쌓입니다.

주의: 옮긴 스킬 본문 안에서 서로를 부를 때는 원래 짧은 이름(`/update-docs`, `/brief` 같은)을 그대로 씁니다. 키트에서 이름 앞에 붙인 접두어와 안 맞으니, 키트에 넣을 때 본문의 호출 이름을 새 이름으로 맞춰야 바로 돕니다.

키트와 붙이는 자세한 자리는 [`convengers/연결.md`](convengers/연결.md) 에 적었습니다.

원저작: VIBE MAFIA CLUB (https://github.com/vibemafiaclub/mafia-codereview-harness). 라이선스는 원본 README의 License 절(MIT) 그대로입니다. 아래 원문과 저작권 표기는 손대지 않았습니다.

---

# MAFIA Code-Review harness

![flow.png](./assets/flow.png)

Claude Code 기반 코드리뷰 자동화 파이프라인.

> Git과 함께 사용할 때 가장 효과적입니다.

> 하네스와 파이프라인에 대한 자세한 설명은 [영상](https://www.youtube.com/watch?v=CfLhrS0ww5w)을 참고해주세요.

## Quick Start

1. 플러그인을 설치합니다.

   ```sh
   # claude code 실행
   claude

   # 플러그인 설치
   /plugin marketplace add vibemafiaclub/mafia-codereview-harness
   /plugin install mafia-codereview
   ```

2. `docs/code-convention.yaml`과 `docs/adr.yaml`를 복사한 뒤, 상황에 맞게 수정합니다.
3. Claude Code에서 `/mafia-codereview:auto`를 실행하세요.

## 파이프라인 흐름

```
/mafia-codereview:auto 실행
  → [1] 상태 점검 (base branch 확인)
  → [2] 설계의도 작성 (Fork)
  → [3] 평가기준 수립 (Fork + Sub-agent)
  → [4] PR 본문 생성 (Fork)
  → [5] 코드리뷰 실행 (Sub-agent, 자동)
  → [6] 리뷰 반영 + QA (Fork)
```

## Skill 목록

| 커맨드                             | 설명                            |
| ---------------------------------- | ------------------------------- |
| `/mafia-codereview:auto`           | 전체 파이프라인 오케스트레이션  |
| `/mafia-codereview:write-intent`   | 설계의도 문서 작성              |
| `/mafia-codereview:gen-criteria`   | 평가기준 자동 생성              |
| `/mafia-codereview:create-pr-body` | PR 본문 생성                    |
| `/mafia-codereview:review`         | 코드리뷰 실행                   |
| `/mafia-codereview:reflect-review` | 리뷰 반영 + QA                  |
| `/mafia-codereview:update-docs`    | code-convention / ADR 항목 관리 |

## 산출물

작업별 산출물은 `.review-artifacts/{branch-name}/`에 저장됩니다.

## License

MIT
