# Deploy Deep Seek on Ubuntu 24.04

## Ollama

## vLLM

### 1. Create new Python environment
```bash
python3 -m venv deepseek-env
```

### 2. Activate Python environment
```bash
source deepseek-env/bin/activate
```

### 3. Install vLLM from pip:
```bash
pip install vllm
```

### 4. Load and run the model:
```bash
vllm serve "ModelCloud/DeepSeek-R1-Distill-Qwen-7B-gptqmodel-4bit-vortex-v2"
```

### 5. Call the server using curl:
```bash
curl -X POST "http://localhost:8000/v1/chat/completions" \
	-H "Content-Type: application/json" \
	--data '{
		"model": "ModelCloud/DeepSeek-R1-Distill-Qwen-7B-gptqmodel-4bit-vortex-v2",
		"messages": [
			{
				"role": "user",
				"content": "What is the capital of France?"
			}
		]
	}'
```
