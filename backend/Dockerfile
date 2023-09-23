# Use a imagem de desenvolvimento Rust para compilar o projeto Actix-web
FROM ekidd/rust-musl-builder AS builder

# Define o diretório de trabalho
WORKDIR /app

# Copie o código-fonte do backend para o diretório de trabalho
COPY . .

# Compile o projeto Actix-web
RUN cargo build --release --target=x86_64-unknown-linux-musl

# Use uma imagem leve do Alpine Linux para a implantação
FROM alpine:latest

# Instale as dependências necessárias (como OpenSSL)
RUN apk --no-cache add ca-certificates

# Copie o executável compilado do projeto Actix-web da etapa anterior
COPY --from=builder /app/target/x86_64-unknown-linux-musl/release/may_back /app/may_back

# Defina o diretório de trabalho
WORKDIR /app

# Exponha a porta que o servidor Actix-web usará (ajuste conforme necessário)
EXPOSE 8000

# Execute o aplicativo Actix-web
CMD ["./may_back"]

