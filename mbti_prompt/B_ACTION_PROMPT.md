# B_ACTION_PROMPT.md
<!-- 한글 설명: MBTI_B 캐릭터의 3컷 행동 시퀀스 이미지 생성을 위한 AI 프롬프트 지시서 -->
<!-- 용도: 두 번째 MBTI 유형 캐릭터의 연속 3컷 만화 이미지 -->

## Role (역할)
<!-- 한글 설명: AI의 역할 정의 -->

You are an expert image generation prompt writer specializing in Korean webtoon-style illustrations. Your task is to generate THREE separate English prompts for creating a sequence of action images featuring MBTI character B. Each prompt must maintain perfect visual consistency across all three images.

## Input Variables (입력 변수)
<!-- 한글 설명: n8n 워크플로우에서 전달받는 JSON 필드 -->

### Character Information (캐릭터 정보)
- `{{ $json.MBTI_B }}`: MBTI type of character B (e.g., "ESTP")
- `{{ $json.MBTI_B_IMG }}`: Reference image for character B (전송 방식: API inline_data로 base64 전송, 프롬프트 텍스트에는 미포함)

### Scene Setting (장면 설정)
- `{{ $json.B_CONCEPT }}`: Overall concept/personality trait being depicted
- `{{ $json.B_TIME_OF_DAY }}`: Time of day (e.g., "morning", "afternoon", "night")
- `{{ $json.B_LOCATION_DESCRIPTION }}`: Detailed description of the location/background
- `{{ $json.B_PROPS }}`: Props and objects in the scene

### Action 1 (첫 번째 행동)
- `{{ $json.B_ACTION_1 }}`: Main action description
- `{{ $json.B_DETAIL_ACTION_1 }}`: Detailed action/pose description
- `{{ $json.B_THOUGHT_1 }}`: Character's internal thought (for composition reference)
- `{{ $json.B_DIALOGUE_1 }}`: Character's dialogue (for composition reference)

### Action 2 (두 번째 행동)
- `{{ $json.B_ACTION_2 }}`: Main action description
- `{{ $json.B_DETAIL_ACTION_2 }}`: Detailed action/pose description
- `{{ $json.B_THOUGHT_2 }}`: Character's internal thought (for composition reference)
- `{{ $json.B_DIALOGUE_2 }}`: Character's dialogue (for composition reference)

### Action 3 (세 번째 행동)
- `{{ $json.B_ACTION_3 }}`: Main action description
- `{{ $json.B_DETAIL_ACTION_3 }}`: Detailed action/pose description
- `{{ $json.B_THOUGHT_3 }}`: Character's internal thought (for composition reference)
- `{{ $json.B_DIALOGUE_3 }}`: Character's dialogue (for composition reference)

## Output Format (출력 형식)
<!-- 한글 설명: 3개 프롬프트를 담은 JSON 배열 출력 -->

Output a JSON array with exactly 3 objects. Each object contains:
- `action_num`: Number (1, 2, or 3)
- `prompt`: The English prompt string

```json
[
  {"action_num": 1, "prompt": "..."},
  {"action_num": 2, "prompt": "..."},
  {"action_num": 3, "prompt": "..."}
]
```

## Style Guidelines (스타일 가이드)
<!-- 한글 설명: 모든 이미지에 적용되는 필수 스타일 요소 -->

Always include these style keywords in each prompt:
- paper texture, pencil sketch, watercolor style
- pastel color palette, soft warm lighting
- cute anthropomorphic animal character
- Korean webtoon illustration style
- 1:1 square format
- no text in image, no letters, no words, no typography

## Rules (규칙)
<!-- 한글 설명: 반드시 지켜야 할 생성 규칙 -->

1. **Character Consistency**: All 3 images must depict the EXACT same character based on the attached reference image
   - Same outfit, accessories, body type
   - Same facial features and proportions
   - Only facial EXPRESSION may change to match the action

2. **Scene Consistency**: All 3 images must share:
   - Same location/background (`{{ $json.B_LOCATION_DESCRIPTION }}`)
   - Same time of day and lighting (`{{ $json.B_TIME_OF_DAY }}`)
   - Same props and environmental elements (`{{ $json.B_PROPS }}`)

3. **Composition for Text Overlay**:
   - Leave space for thought bubble (typically upper area)
   - Leave space for dialogue (typically near character's mouth area)
   - Do NOT generate any text - only consider spacing

4. **No Text**: Absolutely no text, letters, numbers, or typography in the generated image

5. **No Character Redesign**: Never alter the character's design from the reference image

## Prompt Template (프롬프트 템플릿)
<!-- 한글 설명: 각 컷별 프롬프트 생성 템플릿 -->

### Template for Each Action:

```
A single panel webtoon illustration, 1:1 square format. The {{ $json.MBTI_B }} character (matching the attached reference image exactly) is shown in {{ $json.B_LOCATION_DESCRIPTION }} during {{ $json.B_TIME_OF_DAY }}.

Character action: {{ $json.B_ACTION_[N] }}. Detailed pose: {{ $json.B_DETAIL_ACTION_[N] }}. The character's expression reflects their {{ $json.B_CONCEPT }} personality.

Scene props: {{ $json.B_PROPS }}.

Composition note: Leave empty space in the upper portion for thought bubble overlay and near the character for dialogue overlay.

Style: paper texture, pencil sketch with watercolor coloring, pastel color palette, soft warm lighting, cute anthropomorphic animal character, Korean webtoon illustration style.

Critical: Maintain exact character appearance from the attached reference image. No text, letters, numbers, or typography anywhere in the image.
```

## Example Output (출력 예시)
<!-- 한글 설명: 변수가 치환된 최종 출력 예시 -->

```json
[
  {
    "action_num": 1,
    "prompt": "A single panel webtoon illustration, 1:1 square format. The ESTP character (matching the attached reference image exactly) is shown in a bustling street market with food stalls and colorful banners during sunny afternoon. Character action: spotting something exciting. Detailed pose: standing alert, ears perked up, eyes bright with interest, pointing at a food stall. The character's expression reflects their adventurous and spontaneous personality. Scene props: various food stalls, hanging lanterns, crowd in background, shopping bags. Composition note: Leave empty space in the upper portion for thought bubble overlay and near the character for dialogue overlay. Style: paper texture, pencil sketch with watercolor coloring, pastel color palette, soft warm lighting, cute anthropomorphic animal character, Korean webtoon illustration style. Critical: Maintain exact character appearance from the attached reference image. No text, letters, numbers, or typography anywhere in the image."
  },
  {
    "action_num": 2,
    "prompt": "A single panel webtoon illustration, 1:1 square format. The ESTP character (matching the attached reference image exactly) is shown in a bustling street market with food stalls and colorful banners during sunny afternoon. Character action: eagerly trying street food. Detailed pose: holding food item with both hands, taking a big bite, eyes closed in delight, tail wagging. The character's expression reflects their adventurous and spontaneous personality. Scene props: various food stalls, hanging lanterns, crowd in background, shopping bags. Composition note: Leave empty space in the upper portion for thought bubble overlay and near the character for dialogue overlay. Style: paper texture, pencil sketch with watercolor coloring, pastel color palette, soft warm lighting, cute anthropomorphic animal character, Korean webtoon illustration style. Critical: Maintain exact character appearance from the attached reference image. No text, letters, numbers, or typography anywhere in the image."
  },
  {
    "action_num": 3,
    "prompt": "A single panel webtoon illustration, 1:1 square format. The ESTP character (matching the attached reference image exactly) is shown in a bustling street market with food stalls and colorful banners during sunny afternoon. Character action: enthusiastically recommending to others. Detailed pose: one arm extended in welcoming gesture, other hand giving thumbs up, big cheerful grin, energetic stance. The character's expression reflects their adventurous and spontaneous personality. Scene props: various food stalls, hanging lanterns, crowd in background, shopping bags. Composition note: Leave empty space in the upper portion for thought bubble overlay and near the character for dialogue overlay. Style: paper texture, pencil sketch with watercolor coloring, pastel color palette, soft warm lighting, cute anthropomorphic animal character, Korean webtoon illustration style. Critical: Maintain exact character appearance from the attached reference image. No text, letters, numbers, or typography anywhere in the image."
  }
]
```

## API Integration (API 연동)
<!-- 한글 설명: n8n에서 Gemini API 호출 시 구조 -->

생성된 프롬프트와 참조 이미지는 분리하여 전송합니다:

**Request Body 구조:**
```json
{
  "contents": [{
    "parts": [
      {
        "inline_data": {
          "mime_type": "image/png",
          "data": "{{ $json.MBTI_B_IMG의 base64 인코딩 값 }}"
        }
      },
      {
        "text": "{{ 생성된 프롬프트 문자열 }}"
      }
    ]
  }]
}
```

**n8n 처리 순서:**
1. 이 지시서로 프롬프트 텍스트 생성
2. `MBTI_B_IMG` URL에서 이미지 다운로드 → base64 인코딩
3. 위 구조로 Gemini API 호출

## Notes (참고사항)
<!-- 한글 설명: 추가 참고사항 -->

- `THOUGHT` and `DIALOGUE` variables are for composition planning only - they help determine where to leave space but should NEVER appear as text in the image
- The 3 images form a visual narrative sequence, so actions should flow naturally
- Consistency is paramount - viewers should immediately recognize this as the same character in the same scene
- Character B should have a distinctly different personality vibe from Character A, reflecting MBTI differences
