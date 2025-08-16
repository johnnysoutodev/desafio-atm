FROM node:18-alpine

WORKDIR /app

# Copiar package.json primeiro (para cache das dependências)
COPY package*.json ./

# Instalar dependências
RUN npm ci --only=production

# Copiar código da aplicação
COPY . .

# Criar diretório de dados se não existir
RUN mkdir -p data

# Expor porta
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD node healthcheck.js || exit 1

# Comando para iniciar
CMD ["npm", "start"]