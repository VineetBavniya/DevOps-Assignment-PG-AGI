#build stage 
FROM node:18 AS builder 

WORKDIR /app/frontend

COPY package*.json . 

RUN npm install 

COPY . .


#Final step 
FROM node:18-slim AS runner

WORKDIR /app

# create User 
RUN adduser --disabled-password appuser

# Copy from builder
COPY --from=builder /app/frontend .

# Install only production deps (still as root)
RUN npm install --omit=dev

# Change ownership of files to new user
RUN chown -R appuser /app

# Switch to non-root user
USER appuser


EXPOSE 3000

CMD ["npm", "run", "dev"]
