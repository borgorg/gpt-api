# GPT-API

[![npm Package Version](https://img.shields.io/npm/v/node-gpt-api)](https://www.npmjs.com/package/node-gpt-api)
[![PyPi Package Version](https://img.shields.io/pypi/v/gpt-api-python)](https://pypi.org/project/gpt-api-python)

GPT-API - a library providing an API for developers to integrate GPT's AI-powered conversational features into applications developed in any programming language (without OpenAI API key nor VPN).

<figure style="text-align:center">
<img alt="A developer working with a laptop and a mini robot assistant standing on the table" src="https://image2.cdn2.seaart.ai/2023-07-25/48738386387013/7d7e69e04161e8da19cd1b1f4c08e077af90cb1a.png" style="max-width: 50ch">
<figcaption>
Illustration Source: https://www.seaart.ai/explore/detail/civigtp4msb4urco4c5g
</figcaption>
</figure>

## Remarks

The spirit of this library is to enable developers to use the Platform for Open Exploration (Poe) via API. It's designed to empower integration and application development within the terms of service of Poe, which specifically disallow any form of automation that exceeds the set rate limits. Please use this library responsibly and within the provided guidelines.

## Features

- **Intuitive API**: Make conversation with GPT models via simple and developer-friendly API.

- **Programming Language Agnostic**: Designed to work with any programming language. Integrate GPT-powered conversational functionalities into your existing projects with ease.

- **Responsible Usage**: Encourages users to respect the guidelines and rate limits set by Poe.

## Installation

Depending on your programming language of choice, use the corresponding package manager to install GPT-API.

```bash
# For Node.js
npm install node-gpt-api

# For Python
pip install gpt-api-python
```

## Usage Examples

### Calling GPT-API from Python

```python
# Import functions from the Python package
from gpt_api import ask
from gpt_api.cli import clear_screen

# ask GPT a question and wait for complete response
task = ask(question='Can I call GPT API from python?')
file_path = f"task-{task['id']}.html"
with open(file_path, 'w') as file:
	file.write(task['html'])
print(task['text'])


# ask GPT a question and process the partial response in realtime
def show_progress(task):
	clear_screen()
	print(task['question'])
	print('=' * 32)
	print(task['text'])

# Use the chat method
task = gpt.chat(prompt='What can I do with GPT?', callback=show_progress)
print(f"text: {len(task['text'])}, html: {len(task['html'])}")
```

Detail example can refer to the demo [cli.py](./client/python/src/gpt_api/cli.py)

### Calling GPT-API from Typescript

```typescript
import { ask } from 'node-gpt-api'
import { writeFileSync } from 'fs'

async function main() {
  // ask GPT a question and wait for complete response
  let task = await ask('Can I call GPT API from Typescript?')
  console.log(task.text)
  writeFileSync(`task-${task.id}.html`, task.html)

  // ask GPT a question and process the partial response in realtime
  task = await ask('What can I do with GPT?', task => {
    console.clear()
    console.log(task.question)
    console.log('='.repeat(32))
    console.log(task.text)
  })
  console.log('text:', task.text.length, 'html:', task.html.length)
}
main()
```

Detail example can refer to the demo [cli.ts](./client/typescript/cli.ts)

## API Endpoints

The API endpoint can be used directly if the SDK for your programming language is not available.

API origin: http://localhost:8041

| HTTP Method | Url            | Remark                                                                            |
| ----------- | -------------- | --------------------------------------------------------------------------------- |
| POST        | /tasks         | create new task with "question" in body                                           |
| GET         | /tasks/pending | used by the userscript internally to get pending task                             |
| PATCH       | /tasks/:id     | used by the userscript internally to update partial response                      |
| GET         | /tasks/:id     | get task response (text and html), with "?completed=true" to wait until completed |
| DELETE      | /tasks/:id     | delete/cancel task                                                                |

Details can see the APIs with Insomnia. ([config file: api/Insomnia.json](./api/Insomnia.json))

Side Note:
The port number was suggested by GPT: 80 stands for Bot (t was omitted); 41 stands for A1. The digit characters look similar to the english characters.

## Proper Use

It's important to note that Poe's terms of service disallow any form of automation that exceeds the rate limits set forth by Poe. Please ensure to use this library responsibly and within the limits set by Poe. Improper use may lead to suspension of your access to the services.

## Potential Use Cases

(This section is generated by GPT-4 itself)

GPT (Generative Pre-trained Transformer) models are powerful language models capable of generating human-like text. They can be used to enable a wide range of functionalities:

- **Chatbots and Conversational Agents**: GPT models can be used to create chatbots that can carry on human-like conversations. These chatbots can answer questions, provide recommendations, and even have friendly chats with users.

- **Text Generation and Completion**: Given a prompt, GPT models can generate coherent and contextually relevant text. This can be used for tasks such as writing essays, generating code, creating poetry, and much more.

- **Translation**: While not specifically trained for translation, GPT models have shown reasonable performance in translating text between languages.

- **Summarization**: GPT models can be used to summarize long pieces of text, providing a condensed version while preserving the original meaning.

- **Question Answering**: Given a context and a question, GPT models can provide accurate answers, making them useful for tasks like customer support, tutoring, and knowledge extraction.

- **Sentiment Analysis**: While not a primary use case, GPT models can be used to analyze the sentiment of a piece of text, identifying whether the sentiment is positive, negative, or neutral.

- **Content Moderation**: GPT models can help moderate content, identifying inappropriate or offensive text.

- **Personal Assistants**: GPT models can be used to create personal assistants that can schedule appointments, send messages, set reminders, and more.

- **Tutoring**: GPT can provide detailed explanations on a wide range of topics, making it a useful tool for education and tutoring.

These applications can be integrated into various software applications, websites, and services to provide a more interactive and personalized user experience.

However, it's important to note that while GPT models are powerful, they are not perfect. They can sometimes generate incorrect or inappropriate responses, and should not be relied upon for critical decision-making without human supervision.

## License

This project is licensed with [BSD-2-Clause](./LICENSE)

This is free, libre, and open-source software. It comes down to four essential freedoms [[ref]](https://seirdy.one/2021/01/27/whatsapp-and-the-domestication-of-users.html#fnref:2):

- The freedom to run the program as you wish, for any purpose
- The freedom to study how the program works, and change it so it does your computing as you wish
- The freedom to redistribute copies so you can help others
- The freedom to distribute copies of your modified versions to others
