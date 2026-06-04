# Projeto: Guia de Construção de um Home Lab Eficiente

## Miniguia de Estudos: Arquitetura de Home Lab (Proxmox e ZFS)

## 1. Contexto e Objetivos
Este projeto foi desenvolvido utilizando o NotebookLM para realizar a curadoria e síntese de informações técnicas sobre a montagem de um Home Lab resiliente. O foco é compreender a camada de virtualização e o gerenciamento de armazenamento de alta integridade.

 ** 1.1 - Objetivos de Estudo:**
  - Dominar a virtualização com Proxmox VE.
  - Implementar armazenamento seguro e redundante utilizando o sistema de arquivos ZFS.

## 2. Curadoria de Fontes
## 2.1 - Utilizei as seguintes documentações técnicas oficiais para alimentar a base de conhecimento no NotebookLM:
1. **Proxmox VE Administration Guide:** [https://pve.proxmox.com/pve-docs/pve-admin-guide.html](https://pve.proxmox.com/pve-docs/pve-admin-guide.html)
2. **OpenZFS Documentation:** [https://openzfs.github.io/openzfs-docs/](https://openzfs.github.io/openzfs-docs/)

## 2.2 - Arquivos PDF
1. **Caixa_de_Ferramentas_DevOps_Um_Guia_para_Construção,_Administração.pdf:** Um guia sobre ferramentas de automação e virtualização, como Ansible e Vagrant.
2. **Containers_com_Docker_Do_desenvolvimento_à_produção_Autor_Casa_do.pdf:** Explica o uso de Docker, sistemas de arquivos em camadas e gerenciamento de volumes.
3. **Entrega_Contínua_Como_Entregar_Software_de_Forma_Rápida_e_Confiável.pdf:** Trata de engenharia de software, pipelines de implantação e automação de testes.
4. **Hardware de Computadores 1.pdf:** Aborda componentes físicos como memórias RAM, ROM, HDs, SSDs e conectores.
5. **Kubernetes_Tudo_sobre_orquestração_de_contêineres_Autor_Casa_do.pdf:** Guia completo sobre orquestração de contêineres, pods, clusters e deployments.
6. **Linux-a-biblia-pt-br.pdf:** Um guia extenso sobre o sistema operacional Linux, desde comandos básicos até administração de servidores e segurança.
7. **SQL-para-Análise-de-Dados.pdf:** Focado em técnicas avançadas de SQL para transformar dados em insights e realizar limpezas de dados.

## 2.3 - Vídeos (YouTube)
1. **Como começar no Homelab do Zero? - Guia para Iniciantes:** Vídeo do canal Diolinux que discute opções de sistemas para servidores e virtualização, como Proxmox e TrueNAS.
2. **JORNADA PROXMOX - YouTube:** Uma playlist (curso completo) que ensina passo a passo a instalação, configuração de clusters e alta disponibilidade no Proxmox VE.
3. **Montando meu HOMELAB - Parte 1: O problema: Vídeo de Emerson Seiler sobre o planejamento de um homelab para armazenamento de arquivos e serviços de mídia.
4. **O Proxmox Definitivo pro Homelab!** IA Local, Jogos e GPU Passthrough!: Tutorial do Diolinux focado em configurações avançadas no Proxmox, como armazenamento e GPU Passthrough.
5. **Serviços do meu HOMELAB em 2025:** Vídeo de Slackjeff que apresenta diversos serviços autohospedados, como VPNs (WireGuard), wikis (Bookstack) e servidores de mídia.

## 3. Engenharia de Prompts e "Cicatrizes"
*   **Prompt inicial:** "Crie um passo a passo para instalar o proxmox"
    *   *Resultado:* Para instalar o **Proxmox Virtual Environment (VE)**, siga este passo a passo detalhado baseado na documentação técnica e guias de administração:

### 1. Preparação e Requisitos de Hardware
*   **Processador:** Deve ser de **64 bits** (Intel ou AMD) com suporte a tecnologias de virtualização (**Intel VT-x** ou **AMD-V**) habilitadas na BIOS/UEFI.
*   **Memória RAM:** Recomenda-se um mínimo de **2 GB** para o sistema operacional e serviços do Proxmox, além da memória dedicada para as máquinas virtuais. Para uso profissional ou com sistemas de arquivos avançados como ZFS, 32 GB ou mais são recomendados.
*   **Rede:** Pelo menos uma placa de rede (NIC) é necessária.

### 2. Criação da Mídia de Instalação
*   **Download:** Baixe a imagem ISO oficial (versão PVE) diretamente do site da Proxmox.
*   **Gravação:** Utilize um pendrive de no mínimo **8 GB**. Ferramentas recomendadas incluem **Ventoy**, **Rufus** (utilizando o modo DD), **Etcher** ou **Fedora Media Writer**.

### 3. Iniciando o Instalador
*   **Boot:** Insira o pendrive no servidor, ligue-o e configure a BIOS/UEFI para iniciar pela mídia USB.
*   **Menu Inicial:** Selecione a opção **"Install Proxmox VE (Graphical)"** para usar o instalador gráfico. 
    *   *Dica:* Se houver problemas com o hardware de vídeo e a tela travar, você pode tentar a opção de modo console ou adicionar o parâmetro `nomodeset` nas opções avançadas.
*   **EULA:** Leia e aceite o contrato de licença de usuário final para prosseguir.

### 4. Configuração do Sistema
*   **Seleção de Disco:** Escolha o disco rígido onde o sistema será instalado. No botão **"Options"**, você pode selecionar o sistema de arquivos, como **ext4, XFS ou ZFS**. 
    *   *Nota:* O **ZFS** é ideal se você busca redundância via software (RAID) sem a necessidade de uma controladora de hardware.
*   **Localização:** Selecione o país (**Brazil**), o fuso horário (**America/Sao_Paulo**) e o layout do teclado (**Brazil-Portuguese**).
*   **Senha e E-mail:** Defina uma senha forte para o usuário **root** (administrador) e insira um e-mail válido para receber alertas e notificações do sistema.
*   **Rede (Management Interface):**
    *   Selecione a placa de rede principal.
    *   Defina o **Hostname (FQDN)** (ex: `pve01.exemplo.com`).
    *   Atribua um **IP fixo** (estático), máscara de rede, Gateway e servidor DNS.

### 5. Finalização
*   **Resumo:** Revise todas as informações na tela de resumo. Se tudo estiver correto, clique em **"Install"**.
*   **Reboot:** Após o término da cópia dos arquivos, o servidor reiniciará automaticamente. **Remova o pendrive** para garantir que o sistema inicie pelo disco rígido.

### 6. Primeiro Acesso e Pós-Instalação
*   **Acesso Web:** Em outro computador conectado à mesma rede, abra o navegador e acesse o endereço IP configurado na porta **8006** usando HTTPS: `https://[IP_DO_SERVIDOR]:8006`.
*   **Login:** Utilize o usuário **root** e a senha definida durante a instalação.
*   **Armazenamento e ISOs:** Se houver discos adicionais, você pode inicializá-los no menu **"Disks"**. Vá em seu storage local e selecione **"ISO Images"** para fazer o upload dos sistemas operacionais que deseja virtualizar.
*   **Prompt refinado:** "Atue como um especialista em sistemas de armazenamento. Com base nos documentos fornecidos, explique a diferença entre RAID tradicional e ZFS no Proxmox, destacando os mecanismos de proteção contra corrupção de dados (data scrubbing)."
    *   **"Cicatriz" (Troubleshooting):** A IA sugeriu pools de armazenamento complexos que exigiam mais discos do que eu tinha disponível. Tive que ajustar o prompt para: *"Considere um cenário de Home Lab com um pool de discos limitado (ex: espelhamento/mirror), focando em custo-benefício e segurança"*. O aprendizado aqui foi que a estrutura de armazenamento deve ser pensada conforme o hardware físico disponível.

## 4. Miniguia de Estudo (Entrega Final)

### Resumo Estruturado
*   **Proxmox VE:** Gerencia hypervisors KVM e containers LXC, permitindo isolar serviços em um único servidor físico.
*   **ZFS:** Utiliza o conceito de "Copy-on-Write" (CoW), o que significa que ele nunca sobrescreve dados, prevenindo perda de informações durante falhas elétricas.
*   **Gestão de Dados:** A combinação de snapshots no Proxmox com a estrutura do ZFS permite recuperação de desastres extremamente rápida.

### Glossário
*   **Hypervisor:** Software que permite executar várias máquinas virtuais simultaneamente no mesmo hardware.
*   **Pool (ZFS):** A unidade de armazenamento lógica que agrupa seus discos rígidos.
*   **Scrubbing:** Processo de verificação de integridade do ZFS que busca e repara erros silenciosos nos dados.

### Prompts Reutilizáveis
1. "Explique as melhores práticas para monitorar a saúde dos discos em um pool ZFS dentro do Proxmox."
2. "Com base nos docs, qual é o impacto de performance ao ativar compressão LZ4 em um dataset ZFS no Proxmox?"
