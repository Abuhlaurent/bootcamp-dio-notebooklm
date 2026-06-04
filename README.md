# Projeto: Guia de Construção de um Home Lab Eficiente

## 1. Contexto e Objetivos
Este projeto foi desenvolvido como um caderno temático no NotebookLM para consolidar os conhecimentos necessários para a construção de um Home Lab moderno e resiliente. O objetivo principal é estudar a arquitetura de servidores locais, virtualização e automação.
- **Objetivos de Estudo:**
  - Entender a implementação de sistemas de virtualização (Proxmox).
  - Estudar a gestão de arquivos e redundância (ZFS).
  - Aprender a automatizar processos de infraestrutura (n8n).

## 2. Curadoria de Fontes
Utilizei documentos técnicos oficiais e guias de boas práticas para alimentar o NotebookLM:
1. **Proxmox VE Administration Guide:** [https://pve.proxmox.com/pve-docs/pve-admin-guide.html](https://pve.proxmox.com/pve-docs/pve-admin-guide.html)
2. **ZFS OpenZFS documentation:** [https://openzfs.github.io/openzfs-docs/](https://openzfs.github.io/openzfs-docs/)
3. **n8n Workflow Automation Docs:** [https://docs.n8n.io/](https://docs.n8n.io/)

## 3. Engenharia de Prompts e "Cicatrizes"
*   **Prompt inicial:** "Como montar um servidor?"
    *   *Resultado:* Muito genérico.
*   **Prompt refinado:** "Atue como um arquiteto de infraestrutura. Explique, com base nos docs do Proxmox e ZFS, as vantagens de utilizar ZFS em um ambiente virtualizado de Home Lab, considerando segurança e integridade de dados."
    *   **"Cicatriz" (Dificuldade/Troubleshooting):** A IA inicialmente sugeriu configurações de hardware de nível empresarial que não eram ideais para meu laboratório doméstico. Tive que restringir o prompt adicionando: *"Considere um cenário de Hardware Proxmox em uma configuração de servidor único com ZFS"*. Isso trouxe respostas mais aplicáveis à minha realidade.

## 4. Miniguia de Estudo (Entrega Final)

### Resumo Estruturado
*   **Virtualização:** O Proxmox VE é a base para gerenciar recursos (CPU/RAM) de forma eficiente.
*   **Armazenamento:** ZFS é a escolha ideal pela proteção contra corrupção de dados (Copy-on-Write).
*   **Automação:** O n8n atua como a camada de inteligência, permitindo disparar fluxos baseados em logs do sistema.

### Glossário
*   **ZFS (Zettabyte File System):** Sistema de arquivos que combina gestão de volumes e sistema de arquivos, focado em integridade.
*   **RAG (Retrieval-Augmented Generation):** Técnica de alimentar uma IA com documentos específicos (como fiz no NotebookLM).
*   **Hypervisor:** Camada de software (ex: Proxmox) que cria e gerencia máquinas virtuais.

### Prompts Reutilizáveis
1. "Com base na documentação, quais são os melhores procedimentos para manter a integridade dos dados no ZFS após uma queda de energia?"
2. "Crie um checklist de segurança básico para um servidor exposto apenas via VPN, considerando as melhores práticas do Proxmox."
