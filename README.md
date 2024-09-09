# Text Generation Web UI API

This is a modified version of the oobabooga/text-generation-webui project, adapted to serve as a general-purpose API for text generation. While originally created for the Montenegrin AI Chef project, this API can be used for any application requiring natural language processing capabilities.

## Features

* OpenAI-compatible API server with Chat and Completions endpoints.
* Multiple backends for text generation in a single API, including Transformers, llama.cpp (through llama-cpp-python), ExLlamaV2, AutoGPTQ, and TensorRT-LLM.
* Automatic prompt formatting for each model using the Jinja2 template in its metadata.
* Easy switching between different models through the API without restarting.
* Versatile application: Suitable for chatbots, content generation, language translation, and more.

## Installation

1. Clone the repository:
   git clone https://github.com/Perpernet/text-generation-webui-api.git
   cd text-generation-webui-api

2. Create a virtual environment (optional but recommended):
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`

3. Install the required packages:
   pip install -r requirements.txt

4. Download a language model (e.g., a GGUF model for llama.cpp):
   python download-model.py organization/model
   Replace `organization/model` with the actual model you want to use.

## Usage

1. Start the API server:
   python server.py --api --model MODEL_NAME
   Replace MODEL_NAME with the name of the model you downloaded.

2. The API will be available at http://localhost:5000 by default.

3. To use the API with your project, set the base URL to point to your local API server:
   BASE_URL = "http://localhost:5000/v1"

## API Documentation

The API follows the OpenAI API format. Here are the main endpoints:

- /v1/chat/completions (POST): For chat-based completions
- /v1/completions (POST): For text completions

Example usage with Python requests:

import requests

response = requests.post(
    "http://localhost:5000/v1/chat/completions",
    json={
        "model": "MODEL_NAME",
        "messages": [
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "Hello, how are you?"}
        ]
    }
)

print(response.json())

For more detailed API documentation, please refer to the OpenAI API documentation, as this API aims to be compatible with that format.

## Configuration

You can configure the API server using command-line arguments. Some useful options include:

- --api-port API_PORT: Set the API port (default is 5000)
- --model MODEL: Specify the model to load
- --gpu-memory GPU_MEMORY: Limit GPU memory usage
- --cpu: Use CPU for inference instead of GPU

For a full list of options, run:
python server.py --help

## Troubleshooting

If you encounter any issues:

1. Make sure you have the latest version of the code.
2. Check that your model is correctly placed in the `models` directory.
3. Verify that you have installed all required dependencies.
4. If using GPU, ensure you have compatible CUDA drivers installed.

For more help, please open an issue on the GitHub repository.

## License

This project is licensed under the same terms as the original text-generation-webui project. Please refer to the LICENSE file for more details.

## Acknowledgments

- oobabooga for the original text-generation-webui project.
- The Hugging Face team for their Transformers library.
- All contributors to the various model backends used in this project.

## Contributing

Contributions to improve the API or its documentation are welcome. Please feel free to submit issues or pull requests.