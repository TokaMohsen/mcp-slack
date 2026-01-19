FROM node:22.12-alpine AS builder

WORKDIR /build

# Copy package files first for better caching
COPY package*.json ./
COPY tsconfig.docker.json ./tsconfig.json

# Install dependencies (skip scripts to avoid premature build)
RUN npm ci --ignore-scripts

# Copy source code
COPY index.ts ./

# Build the project
RUN npm run build

# Production stage
FROM node:22-alpine AS release

# Add security labels
LABEL maintainer="MCP Slack Server" \
      description="MCP server for interacting with Slack" \
      version="0.1.0"

# Create a non-root user and group
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001 -G nodejs

# Set working directory
WORKDIR /app

# Copy built files and dependencies with proper ownership
COPY --from=builder --chown=nodejs:nodejs /build/dist ./dist
COPY --from=builder --chown=nodejs:nodejs /build/package*.json ./

ENV NODE_ENV=production

# Install only production dependencies
RUN npm ci --ignore-scripts --omit-dev && \
    npm cache clean --force

# Switch to non-root user
USER nodejs

# Expose port if your MCP server uses one (adjust or remove if not needed)
# EXPOSE 3000

# Add healthcheck (optional - adjust based on your server's health endpoint)
# HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
#   CMD node -e "require('http').get('http://localhost:3000/health', (r) => {process.exit(r.statusCode === 200 ? 0 : 1)})"

ENTRYPOINT ["node", "dist/index.js"]
