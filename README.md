# E-Commerce Module Federation

This repository demonstrates a modern **microfrontend architecture** using **Module Federation** with **Bun** as the runtime and package manager.

## 🏗️ Architecture Overview

This project implements the **Multi-Provider, Single Consumer** pattern:
- **1 Consumer**: Main application that imports components from multiple providers
- **2 Providers**: Specialized modules that expose domain-specific functionality

```
mf-ecommerce-consumer (Consumer)
    ↑ imports components from
├── mf-payment-provider (Provider)
└── mf-product-provider (Provider)
```

## 📦 Modules

### **mf-ecommerce-consumer** (Consumer)
- 🎯 **Purpose**: Main e-commerce application that orchestrates the entire user experience
- 📥 **Consumes**: Components from both payment and product providers
- 🏪 **Features**: Complete e-commerce platform, routing, layout, user management

### **mf-payment-provider** (Provider)
- 🎯 **Purpose**: Payment processing and checkout functionality
- 📤 **Exposes**: Payment forms, transaction components, payment methods
- 💳 **Tech Stack**: React, TypeScript, Vite, Module Federation

### **mf-product-provider** (Provider)
- 🎯 **Purpose**: Product catalog and inventory functionality  
- 📤 **Exposes**: Product listings, search components, product details, cart functionality
- 🛍️ **Tech Stack**: React, TypeScript, Vite, Module Federation

## 🚀 Getting Started

### Prerequisites
- **Bun** (latest version)
- **Node.js** 18+ 
- **Git**

### Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd mf-ecommerce
```

2. **Install dependencies for all packages**
```bash
bun run pkg
```

### Development

#### Start all microfrontends
```bash
bun run dev
```

#### Start individual microfrontends
```bash
# Consumer (main app)
bun run dev:mf-ecommerce-consumer

# Payment provider only
bun run dev:mf-payment-provider

# Product provider only
bun run dev:mf-product-provider
```

#### Production build
```bash
bun run build
```

#### Run tests
```bash
bun run test
```

## 🔧 Available Scripts

| Script | Description |
|--------|-------------|
| `bun run dev` | Start all microfrontends in development mode |
| `bun run start` | Start all microfrontends in preview mode |
| `bun run build` | Build all microfrontends for production |
| `bun run test` | Run tests across all projects |
| `bun run pkg` | Install dependencies in all packages |

## 🏛️ Project Structure

```
mf-ecommerce/
├── mf-ecommerce-consumer/     # Consumer module (main app)
├── mf-payment-provider/       # Payment provider module  
├── mf-product-provider/       # Product provider module
├── .vscode/
│   └── launch.json           # VS Code debug configurations
├── package.json              # Root package with workspace scripts
└── README.md
```

## 🐛 VS Code Debugging

This project includes VS Code launch configurations for easy debugging:

1. Open **Run and Debug** (Ctrl+Shift+D)
2. Select from available configurations:
   - Start All Microfrontends (dev)
   - Start All Microfrontends (start)
   - Start Consumer Only (Main App)
   - Start Payment Provider Only
   - Start Product Provider Only
   - Run Tests
   - Install Dependencies

## 🔄 Module Federation Flow

1. **Payment Provider** exposes payment-related components
2. **Product Provider** exposes product-related components  
3. **Consumer** imports and orchestrates components from both providers
4. **TypeScript** definitions ensure type safety across modules
5. **Independent deployment** allows providers to be updated separately

## 🛠️ Tech Stack

- **Runtime**: Bun
- **Frontend**: React + TypeScript
- **Build Tool**: Vite
- **Module Federation**: @originjs/vite-plugin-federation
- **Testing**: Jest
- **Package Management**: Bun workspaces
- **Process Management**: Concurrently

## 🎯 Architecture Benefits

### Multi-Provider Pattern Advantages:
- **Domain Separation**: Payment and product logic are completely separated
- **Team Independence**: Different teams can own payment vs product functionality
- **Specialized Deployment**: Each provider can be deployed independently
- **Focused Responsibility**: Each provider has a single, clear purpose
- **Scalable Integration**: Easy to add more providers (shipping, user management, etc.)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and commit: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## 🆘 Troubleshooting

### Common Issues

**Port conflicts**: Make sure ports 3000, 3001, 3002 are available
```bash
# Check ports
netstat -ano | findstr :3000
```

**Dependencies issues**: Reinstall all packages
```bash
bun run pkg
```

**Build errors**: Clean and rebuild
```bash
bun run build
```

**Module Federation errors**: Ensure all providers are running before starting consumer
```bash
# Start providers first
bun run dev:mf-payment-provider
bun run dev:mf-product-provider

# Then start consumer
bun run dev:mf-ecommerce-consumer
```