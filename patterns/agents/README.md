# 효과적인 에이전트 구축 쿡북 (Building Effective Agents Cookbook)

Erik Schluntz와 Barry Zhang의 [효과적인 에이전트 구축하기](https://anthropic.com/research/building-effective-agents)에 대한 참조 구현체입니다.

이 레포지토리는 블로그에서 논의된 일반적인 에이전트 워크플로우의 최소 구현 예제를 포함하고 있습니다:

- 기본 구성 요소 (Basic Building Blocks)
  - 프롬프트 체이닝 (Prompt Chaining)
  - 라우팅 (Routing)
  - 멀티 LLM 병렬화 (Multi-LLM Parallelization)
- 고급 워크플로우 (Advanced Workflows)
  - 오케스트레이터-서브 에이전트 (Orchestrator-Subagents)
  - 평가자-최적화 도구 (Evaluator-Optimizer)

## 시작하기
상세 예제는 다음 Jupyter 노트북을 참조하십시오:

- [기본 워크플로우 (Basic Workflows)](basic_workflows.ipynb)
- [평가자-최적화 워크플로우 (Evaluator-Optimizer Workflow)](evaluator_optimizer.ipynb) 
- [오케스트레이터-워커 워크플로우 (Orchestrator-Workers Workflow)](orchestrator_workers.ipynb)
    