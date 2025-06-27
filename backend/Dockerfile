# build stage 

FROM python:3.12-slim AS builder 

WORKDIR /app 

COPY requirements.txt .

RUN pip install --user -r requirements.txt 

# Final Stage 

FROM python:3.12-slim 

# create User 
RUN adduser --disabled-password appuser

USER appuser

WORKDIR /home/appuser/app 

# copy packages only installed 
COPY --from=builder /root/.local /home/appuser/.local 

ENV PATH=/home/appuser/.local/bin:$PATH

# Copy source code
COPY --chown=appuser:appuser ./app ./app

# Expose port 
# EXPOSE 8000


CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
