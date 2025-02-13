# Deploy Deep Seek on Ubuntu 24.04

## Prepare

### Install Nvidia Drivers
```bash
sudo apt update
sudo apt install nvidia-driver-535 nvidia-cuda-toolkit
```

## Ollama

### 1. Install Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 2. Run Deep Seek
```bash
ollama serve
ollama run deepseek-r1:7b
```

### 3. REST API
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "deepseek-r1:7b",
  "prompt":"Why is the sky blue?"
}'
```

## vLLM

### 1. Create new Python environment
```bash
python3 -m venv deepseek-env
```

### 2. Activate Python environment
```bash
source deepseek-env/bin/activate
```

### 3. Install vLLM from pip
```bash
pip install vllm
```

### 4. Load and run the model
```bash
vllm serve ModelCloud/DeepSeek-R1-Distill-Qwen-7B-gptqmodel-4bit-vortex-v2 \
    --quantization gptq \
    --gpu-memory-utilization 0.9 \
    --max-model-len 60000 \
    --swap-space 10 \
    --dtype float16 \
    --api-key victor-tang-123
```

### 5. Call the server using curl
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
