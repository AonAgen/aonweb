# AONWeb: Full-Modality Multi-Agent Coordination Framework

Powered by 3,000+ open-source AI models provided by AGI Open Network, AONWeb is a cutting-edge AI Agent framework that offers seamless integration, and advanced coordination to empower developers in building intelligent, full-modality AI systems.

## Core Features

### Web3 Integration
- Smart contract interaction with multiple specialized contracts (AonAgentPoint, AonUser, AonAiModel, etc.)
- Wallet connectivity and authentication
- Token management and reward systems
- Decentralized user management

### AI Agent Capabilities
- Integration with 3000+ state-of-the-art open-source AI models 
- Customizable AI parameters and configurations
- Support for various input/output formats
- Scalable AI execution through clustered architecture

### Technical Architecture
- Modular design with clear separation of concerns
- Environment-specific configurations (development/production)
- Cross-domain storage solutions
- Comprehensive error handling and logging
- Telegram Web App integration

## Key Components

### Smart Contracts
- `AonAppPoint`: Agent point management
- `AonRewardPoint`: Reward system management
- `AonUser`: User identity and permissions
- `AonAiModel`: AI model registry and management
- `AonAiCluster`: Distributed AI processing
- `AonAiExcutor`: AI execution orchestration

### Core Classes
- `AI`: AI model interaction and management
- `AIOptions`: Configuration for AI operations
- `User`: User management and authentication
- `ListOptions`: Data query and pagination
- `Options`: System-wide configuration

## Technical Specifications
- Built with modern JavaScript/TypeScript
- Supports multiple blockchain networks
- RESTful API architecture
- Real-time data processing
- Secure storage handling

## Use Cases
- Decentralized AI Agents
- Token-gated AI capabilities
- AI-powered Web3 Agents
- Custom AI model deployment
- Cross-chain AI interactions

## Future Potential
The framework is designed to evolve into a comprehensive Web3 AI Agent system, supporting:
- Autonomous AI Agents
- Agent-to-agent communication
- Decentralized AI marketplaces
- Token-based governance
- AI model sharing and collaboration

## Security Features
- Secure wallet integration
- Protected API endpoints
- Cross-domain security
- Data encryption
- Smart contract safety checks

## Integration Capabilities
- Easy integration with existing Web3 projects
- Support for multiple AI models
- Extensible plugin system
- Custom contract integration
- Third-party service connectivity

## Quick Start

### Installation
```bash
npm install aonweb
```

### Basic Usage
```javascript
import { AI } from 'aonweb';

// Initialize AI instance
const ai = new AI({
    apiKey: 'your-api-key',
    network: 'mainnet'
});

// Example: Image Generation
async function generateImage() {
    const result = await ai.generateImage({
        prompt: 'A beautiful landscape with mountains',
        model: 'stable-diffusion-v2',
        size: '1024x1024'
    });
    console.log('Generated image URL:', result.url);
}

// Example: Text Generation
async function generateText() {
    const result = await ai.generateText({
        prompt: 'Write a story about AI and blockchain',
        maxTokens: 500
    });
    console.log('Generated text:', result.text);
}
```

## Contributing
We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

AONWeb represents the convergence of Web3 and AI technologies, offering a robust foundation for building the next generation of decentralized AI Agents. Its modular architecture and comprehensive feature set make it an ideal choice for developers looking to create innovative Web3-native AI solutions.

# AONWEB

aonweb - JavaScript sdk for AON

- API version: 1.0.0
- Package version: 1.0.14

## Installation

### For [Node.js](https://nodejs.org/)

#### npm

Install it from npm:

```shell
npm install aonweb --save
```

## Getting Started

Please follow the [installation](#installation) instruction and execute the following JS code:

```javascript

import { AI, AIOptions, User } from 'aonweb'

function sleep(ms) {
	return new Promise(resolve => setTimeout(resolve, ms));
}

function prediction() {
    let user = new User()
    let is_login = await user.islogin()
    if (!is_login) {
        for (let i = 0; i < 10; i++) {
            let result = await user.getOwnedUsers()
            let userid = result && result._userIds && result._userIds.length && result._userIds[0]
            if (userid && userid.length) {
                break
            }
            await sleep(300)       
        }
        is_login = await user.islogin()
        if (!is_login) {
            console.log("login failed,please try again later");
            return
        }
    }
    const ai_options = new AIOptions({
        appId: REPLACE_APP_ID //replace app id
    })
    let price = 10
	const ai = new AI(ai_options)
    let response = await ai.prediction("/predictions/ai/stable-diffusion-3",
    {
        input:{
            "prompt": "with smoke, half ice and half fire and ultra realistic in detail.wolf, typography, dark fantasy, wildlife photography, vibrant, cinematic and on a black background",
            "cfg": 3.5,
            "steps": 28,
            "aspect_ratio": "9:16",
            "output_format": "png",
            "output_quality": 90,
            "negative_prompt": "",
            "prompt_strength": 0.85
        }
    },price);
    if (response && response.code == 200 && response.data) {
        response = response.data
    }
    if (response.task.exec_code == 200 && response.task.is_success) {
        console.log("test",response.output);
    }
}

prediction();

### Constructor

name | type | Description
------------ | ------------- | -------------
*appId* | string | **Required**.
