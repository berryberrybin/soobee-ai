# n8n Gemini API Request Guide

## 이미지 1개 전송 (COVER, A_ACTION, B_ACTION)

```json
{
  "contents": [{
    "parts": [
      {
        "inline_data": {
          "mime_type": "image/png",
          "data": "{{ base64 인코딩된 이미지 }}"
        }
      },
      {
        "text": "{{ 프롬프트 텍스트 }}"
      }
    ]
  }]
}
```

### 변수 매핑
| 프롬프트 | 이미지 변수 |
|---------|-----------|
| COVER_PROMPT | `COVER_IMG` |
| A_ACTION_PROMPT | `MBTI_A_IMG` |
| B_ACTION_PROMPT | `MBTI_B_IMG` |

---

## 이미지 2개 전송 (CONTRAST, CTA)

```json
{
  "contents": [{
    "parts": [
      {
        "inline_data": {
          "mime_type": "image/png",
          "data": "{{ MBTI_A_IMG base64 }}"
        }
      },
      {
        "inline_data": {
          "mime_type": "image/png",
          "data": "{{ MBTI_B_IMG base64 }}"
        }
      },
      {
        "text": "{{ 프롬프트 텍스트 }}"
      }
    ]
  }]
}
```

### 이미지 순서 (중요!)
1. **첫 번째 inline_data** = Character A (`MBTI_A_IMG`) = 프롬프트의 "first attached reference image"
2. **두 번째 inline_data** = Character B (`MBTI_B_IMG`) = 프롬프트의 "second attached reference image"

---

## n8n 처리 흐름

1. 이미지 URL → HTTP Request로 다운로드
2. 다운로드된 바이너리 → Base64 인코딩
3. 프롬프트 텍스트에 변수 치환 (n8n Expression)
4. 위 JSON 구조로 Gemini API 호출

---

## 프롬프트별 필요 변수

### COVER_PROMPT
- (이미지) `COVER_IMG`
- (변수 없음 - 고정 프롬프트)

### A_ACTION_PROMPT
- (이미지) `MBTI_A_IMG`
- `MBTI_A`, `A_LOCATION_DESCRIPTION`, `A_TIME_OF_DAY`
- `A_ACTION`, `A_DETAIL_ACTION`, `A_CONCEPT`, `A_PROPS`

### B_ACTION_PROMPT
- (이미지) `MBTI_B_IMG`
- `MBTI_B`, `B_LOCATION_DESCRIPTION`, `B_TIME_OF_DAY`
- `B_ACTION`, `B_DETAIL_ACTION`, `B_CONCEPT`, `B_PROPS`

### CONTRAST_PROMPT
- (이미지) `MBTI_A_IMG`, `MBTI_B_IMG`
- `MBTI_A`, `MBTI_B`, `SITUATION`, `LOCATION`
- `A_CONCEPT`, `B_CONCEPT`

### CTA_PROMPT
- (이미지) `MBTI_A_IMG`, `MBTI_B_IMG`
- `MBTI_A`, `MBTI_B`
