# APR_DSA
LLM 기반 자동 프로그램 수정(Auto Program Repair) 실험 코드입니다. BugsInPy/Defects4J 버그를 대상로 데이터 정리 → AST+LLM 분석 → BM25 검색 → 프롬프트 생성 → 패치 생성/평가까지 일련의 흐름을 제공합니다.

## 주요 구성
- `0.ControlAgent.py`: 단계별 에이전트(분석/검색/패치/평가) 실행을 오케스트레이션.
- `1.DataSeterAgent*.py`: 메타데이터를 정규화해 `Results/1.DataSeterAgentResult*.json`에 저장.
- `2.LlmASTReasonAnalyzer*.py`: AST 파싱 + (선택적) LLM 추론으로 의심 노드/이유를 생성, `Results/2.*` 저장.
- `3.Bm25*.py`: `rank-bm25`로 유사 버그 검색 결과를 추가, `Results/3.*` 출력.
- `4.GenerateBugfixPrompt*.py`: AST/검색 신호를 조합해 프롬프트 생성, 단일/다중 변이(`4.GeneratePromResult__*.json`) 지원.
- `5.TokenPatchGeneratorAgent.py` 및 `baseline/*.py`: HF 모델로 패치 후보를 생성, 결과는 `Results/patch/*.json`.
- `evaluation/`: BugsInPy/Defects4J 체크아웃·컴파일·테스트 및 pass@k 계산 스크립트.
- `figure/`: 결과 JSON을 기반으로 시각화(heatmap, pass@k 그래프 등).

## 환경 준비
- Python 3.8+ 권장, GPU가 있을 때 `torch`/`transformers` 모델 로딩이 원활합니다.
- 필수 패키지 설치: `pip install -r require.txt` (가상환경 권장).
- 외부 도구: `bugsinpy-*` CLI와 `defects4j`가 PATH에 있어야 평가 스크립트가 동작합니다. 레포 내 `defects4j/` 디렉터리는 배포본이 포함되어 있습니다.
- LLM 체크포인트는 스크립트 기본값(`../DevAgent/qwen1.5-7b-chat` 등)에 맞추어 로컬에 준비하거나, 인자/상수로 경로를 수정하세요.

## 기본 실행 흐름 (BugsInPy/Python)
1) 데이터 정리: `python 1.DataSeterAgent.py`
2) AST+LLM 분석: `python 2.LlmASTReasonAnalyzer.py --input_json Results/1.DataSeterAgentResult.json --output_json Results/2.LLM_Analyzed_Results.json --topk 10` (`--no_model`로 LLM 생략 가능)
3) 유사 버그 검색: `python 3.Bm25.py --all_bugs all_bugs_meta_data.json --real_bugs Results/2.LLM_Analyzed_Results.json --out Results/3.BM25Result.json`
4) 프롬프트 생성: 멀티 변이 예시 `python 4.GenerateBugfixPrompt.py --input Results/3.BM25Result.json --variants full,wo_ast,wo_retrieval --out-dir Results`
5) 패치 생성: `python 5.TokenPatchGeneratorAgent.py --model_name ../DevAgent/qwen1.5-7b-chat --in_file Results/4.GeneratePromResult__full.json --out_file Results/patch/5.PatchesResults.json --num_patches_to_generate 20`

## Java/Defects4J 흐름
- `*_Java.py` 스크립트 세트를 동일한 순서로 실행하면 Defects4J용 JSON과 프롬프트/패치가 생성됩니다 (`Results/*_Java.json`, `Results/patch/*_Java.json` 참고).
- 평가: `python evaluation/Java_evaluate.py --dataset defects4j --model_inference_dirs patch` (필요 시 `--bug_id_list`로 특정 버그만 선택).

## 평가·통계 및 시각화
- BugsInPy 평가: `evaluation/evaluate-Copy1.py`, Java 공용 옵션은 `evaluation/Baseevaluate.py`.
- pass@k 계산: `evaluation/pass_at_k.py`, `evaluation/pass_at_k_Java.py`.
- 시각화: `figure/`의 스크립트는 결과 JSON을 받아 히트맵·그래프를 그립니다(예: `python figure/hitmap.py`).

## 기타
- `Results/`에 샘플 결과와 프롬프트가 포함되어 있어 포맷을 확인할 수 있습니다.
- `temp_workspaces/`는 평가 시 체크아웃되는 임시 프로젝트 경로로, 스크립트에서 자동 정리됩니다.
