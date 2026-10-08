# Arquitetura — DealFlow AI

## Objetivo
SaaS de atendimento e CRM multiempresa. O código de aplicação produzido no Lovable precisa ser exportado e importado antes que a plataforma seja executável a partir deste repositório.

## Stack-alvo
- UI: React + TypeScript + Tailwind
- Persistência e autenticação: PostgreSQL / backend compatível com o projeto original
- Deploy estático: GitHub Pages (somente frontend)
- CI: GitHub Actions

## Segurança não negociável
- Proteger todas as tabelas de negócio por tenant_id e RLS.
- Derivar autorização da sessão autenticada; nunca confiar no tenant_id enviado pelo navegador.
- Usar papéis owner/admin/agent validados no servidor.
- Não versionar .env, tokens, chaves de serviço ou credenciais.
- Nunca publicar service_role nem segredos no build do Pages.
- Testar leitura e escrita cruzada entre empresas antes de comercializar.

## Limites da hospedagem
GitHub Pages não executa PostgreSQL, webhooks nem workers de IA. O frontend publicado deverá apontar para um backend seguro e separado. O WhatsApp oficial e o provedor de IA real requerem configuração independente.

## Testes de aceitação
1. Cadastro/login e renovação de sessão.
2. Criar empresas A e B e verificar isolamento em todas as consultas e mutações.
3. Papéis owner/admin/agent e bloqueios de operação indevida.
4. CRUD de contatos, oportunidades, mensagens e agendamentos.
5. Estados offline/erro, layout Android/iOS/desktop.
6. Build, typecheck, lint e testes automatizados em cada pull request.
