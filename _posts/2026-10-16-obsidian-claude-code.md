---
layout: post
title: "옵시디언 설치부터 Claude Code 연결까지"
summary: 메모 앱 옵시디언을 처음 깔고, Claude Code가 보관함의 메모를 읽고 쓸 수 있게 연결한 과정
tags: [Obsidian, Claude Code, 도구 설정]
---

Claude Code로 작업하다 보면 정리해 둔 메모를 같이 보면서 일하고 싶을 때가 많습니다. 그래서 메모 앱 옵시디언(Obsidian)을 새로 설치하고 Claude Code가 옵시디언 메모를 바로 읽고 쓸 수 있게 연결했습니다. 플러그인이나 별도 서버 없이 설정 한 줄로 끝났습니다.

## 1. 옵시디언 설치

공식 사이트 obsidian.md에서 맥용 설치 파일(.dmg)을 내려받았습니다. 파일을 열면 나오는 창에서 옵시디언 아이콘을 Applications 폴더로 끌어다 놓으면 설치가 끝납니다.

![옵시디언 설치 창: 아이콘을 Applications로 끌어다 놓는다](/assets/img/2026-10-16-obsidian-01-dmg.png)

처음 실행하면 인터넷에서 내려받은 앱이라는 확인 창이 뜹니다. Apple이 악성 소프트웨어 검사를 마친 앱이라 「열기」를 누르면 됩니다.

![인터넷에서 다운로드한 앱을 열지 묻는 확인 창](/assets/img/2026-10-16-obsidian-02-open-warning.png)

## 2. 보관함 만들기

옵시디언은 메모를 **보관함(vault)**이라는 폴더 단위로 관리합니다. 첫 화면에는 선택지가 세 개 있습니다.

| 선택지 | 언제 쓰나 |
|---|---|
| 새 보관함 생성 | 처음 시작할 때 |
| 보관함 폴더 열기 | 이미 마크다운 메모 폴더가 있을 때 |
| Obsidian Sync 보관함 열기 | 유료 동기화를 쓸 때 |

![옵시디언 첫 화면: 새 보관함 생성, 폴더 열기, Sync](/assets/img/2026-10-16-obsidian-03-welcome.png)

처음이라 「새 보관함 생성」을 골랐습니다. 이름과 위치를 정하는 화면이 나옵니다.

![보관함 이름과 위치를 정하는 화면](/assets/img/2026-10-16-obsidian-04-vault-form.png)

위치는 **문서(Documents) 폴더**로 정했습니다. iCloud Drive에 두면 아이폰과 같이 쓰기 편하지만 동기화 중에 파일이 잠깐 비어 보이는 경우가 있어서 처음 연결할 때는 헷갈릴 수 있습니다. 옵시디언도 같은 내용을 안내합니다. 그래서 일단 맥 안에만 두고 나중에 옮기기로 했습니다.

![이름 Obsidian, 위치 문서 폴더로 정한 화면](/assets/img/2026-10-16-obsidian-05-vault-name.png)

「생성」을 누르면 환영 메모 하나가 들어 있는 보관함이 열립니다.

![새 보관함이 열린 화면: 환영 메모와 그래프 뷰](/assets/img/2026-10-16-obsidian-06-vault-open.webp)

## 3. Claude Code에 연결

옵시디언 메모는 특별한 형식이 아니라 **폴더 안의 마크다운(.md) 파일**입니다. 그래서 Claude Code가 그 폴더에 들어갈 수 있게 허락만 해 주면 됩니다.

Claude Code 사용자 설정 파일 `~/.claude/settings.json`에 보관함 폴더를 「추가 작업 폴더」로 적었습니다.

```json
{
  "permissions": {
    "additionalDirectories": ["/Users/(사용자 이름)/Documents/Obsidian"]
  }
}
```

이렇게 해 두면 어느 프로젝트에서 Claude Code를 켜든 옵시디언 보관함을 같이 볼 수 있습니다. 설정 파일을 고치기 전에는 원래 파일을 백업해 두었습니다.

옵시디언 전용 MCP 서버를 쓰는 방법도 있습니다. 하지만 커뮤니티 플러그인과 API 키를 따로 설정해야 합니다. 메모를 읽고 쓰는 것만 필요하다면 폴더 연결이 훨씬 간단합니다.

## 4. 잘 되는지 확인

연결이 됐는지 두 가지로 확인했습니다.

- **읽기**: Claude Code가 보관함에 있던 환영 메모를 읽어 냈습니다.
- **쓰기**: Claude Code가 「Claude Code 연결 확인」 메모를 새로 만들었고 옵시디언 왼쪽 목록에 바로 나타났습니다.

![Claude Code가 만든 「Claude Code 연결 확인」 메모가 옵시디언에 보이는 화면](/assets/img/2026-10-16-obsidian-07-claude-note.webp)

캡처를 보면 제목이 두 번 나옵니다. 옵시디언은 파일 이름을 메모 맨 위에 제목처럼 보여 주는데, Claude Code가 본문 첫 줄에도 `# 제목`을 또 적었기 때문입니다. 옵시디언에 메모를 쓰게 할 때는 본문에 제목 줄을 넣지 말라고 해 두면 깔끔합니다.

## 정리

| 단계 | 한 일 |
|---|---|
| 설치 | obsidian.md에서 내려받아 Applications로 옮김 |
| 보관함 | 문서 폴더에 `Obsidian` 보관함 생성 |
| 연결 | `~/.claude/settings.json`의 `additionalDirectories`에 보관함 경로 추가 |
| 확인 | Claude Code로 메모 읽기·새 메모 만들기 |

이제 Claude Code에게 "옵시디언에 오늘 한 일 정리해 줘"라고 하면 보관함에 바로 메모가 생깁니다.
