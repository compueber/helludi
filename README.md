# Guia de Deploy - Portal HellUdi

## Visão Geral

O Portal do Confrade HellUdi é uma aplicação full-stack composta por:
- **Frontend**: React (Vite) - Hospedagem estática
- **Backend**: Flask API - Hospedagem de aplicação
- **Banco de Dados**: SQLite (incluído no backend)

## Estrutura do Projeto

```
helludi-portal/          # Frontend React
├── dist/               # Build de produção
├── src/               # Código fonte
└── package.json       # Dependências

helludi-api/            # Backend Flask
├── src/               # Código fonte da API
├── database/          # Banco SQLite
└── requirements.txt   # Dependências Python
```

## Deploy do Frontend

### Opção 1: Vercel (Recomendado)

1. **Preparação**:
   ```bash
   cd helludi-portal
   npm run build
   ```

2. **Deploy via Vercel CLI**:
   ```bash
   npm install -g vercel
   vercel --prod
   ```

3. **Configurações necessárias**:
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Install Command: `npm install`

### Opção 2: GitHub Pages

1. **Configurar vite.config.js**:
   ```javascript
   export default defineConfig({
     base: '/helludi-portal/',
     // ... outras configurações
   })
   ```

2. **Build e deploy**:
   ```bash
   npm run build
   # Fazer push do diretório dist para gh-pages branch
   ```

### Opção 3: Netlify

1. **Deploy direto**:
   - Conectar repositório GitHub
   - Build command: `npm run build`
   - Publish directory: `dist`

## Deploy do Backend

### Opção 1: Railway (Recomendado para Flask)

1. **Preparar requirements.txt**:
   ```
   Flask==2.3.3
   Flask-SQLAlchemy==3.0.5
   Flask-CORS==4.0.0
   ```

2. **Criar Procfile**:
   ```
   web: python src/main.py
   ```

3. **Configurar variáveis de ambiente**:
   ```
   PORT=5000
   FLASK_ENV=production
   ```

### Opção 2: Render

1. **Configurações**:
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python src/main.py`

### Opção 3: PythonAnywhere

1. **Upload dos arquivos**
2. **Configurar WSGI**
3. **Instalar dependências**

## Configurações de Produção

### Frontend

1. **Atualizar URLs da API**:
   ```javascript
   const API_BASE_URL = process.env.NODE_ENV === 'production' 
     ? 'https://sua-api.railway.app'
     : 'http://localhost:5000';
   ```

### Backend

1. **Configurar CORS para produção**:
   ```python
   CORS(app, origins=[
     'https://seu-frontend.vercel.app',
     'http://localhost:5173'  # Para desenvolvimento
   ])
   ```

2. **Configurar banco de dados**:
   ```python
   # Para produção, considerar PostgreSQL
   if os.environ.get('DATABASE_URL'):
       app.config['SQLALCHEMY_DATABASE_URI'] = os.environ.get('DATABASE_URL')
   else:
       app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database/app.db'
   ```

## Funcionalidades Implementadas

### ✅ Completas
- [x] Blog com 8 estilos cervejeiros BJCP
- [x] Sistema de usuários e autenticação (estrutura)
- [x] Área de membros com dashboard
- [x] Sistema de assinaturas (R$ 5,00 mensal / R$ 100,00 anual)
- [x] Painel administrativo completo
- [x] API REST completa
- [x] Design responsivo
- [x] Paleta de cores da marca HellUdi

### 🔄 Para Implementar (Próximas Versões)
- [ ] Autenticação Google real
- [ ] Integração PayPal/PIX/Boleto
- [ ] Sistema de notificações por email
- [ ] Backup automático do banco
- [ ] Analytics e métricas avançadas

## URLs de Exemplo

### Desenvolvimento
- Frontend: http://localhost:5173
- Backend: http://localhost:5000

### Produção (após deploy)
- Frontend: https://helludi-portal.vercel.app
- Backend: https://helludi-api.railway.app

## Comandos Úteis

### Desenvolvimento
```bash
# Frontend
cd helludi-portal
npm run dev

# Backend
cd helludi-api
source venv/bin/activate
python src/main.py
```

### Build
```bash
# Frontend
cd helludi-portal
npm run build

# Backend (já pronto para deploy)
cd helludi-api
# Arquivos prontos para upload
```

## Monitoramento

### Métricas Importantes
- Usuários ativos
- Taxa de conversão de assinaturas
- Usuários inadimplentes
- Receita mensal/anual

### Logs
- Acessos ao blog
- Tentativas de login
- Transações de pagamento
- Erros da API

## Suporte

Para dúvidas sobre o deploy ou funcionamento do portal:
1. Verificar logs da aplicação
2. Testar endpoints da API
3. Verificar configurações de CORS
4. Validar variáveis de ambiente

---

**Desenvolvido para a Confraria HellUdi**  
*Compartilhando a cultura cervejeira desde 2013*

