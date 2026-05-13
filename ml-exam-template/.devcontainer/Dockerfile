FROM python:3.12-slim

# Dependencias del sistema
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    git \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Instalar UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh
ENV PATH="/root/.local/bin:${PATH}"

WORKDIR /app

# Crear el entorno virtual
RUN uv venv .venv
ENV VIRTUAL_ENV=/app/.venv
ENV PATH="/app/.venv/bin:${PATH}"

# Instalar dependencias
COPY pyproject.toml uv.lock* /app/
RUN uv pip install --python /app/.venv/bin/python \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    numpy \
    ipykernel \
    jupyter

# Registrar el kernel de Jupyter en el venv
RUN /app/.venv/bin/python -m ipykernel install --name=ml-exam --display-name "Python (ml-exam)"

# Copiar archivos del proyecto
COPY . /app/

CMD ["bash"]