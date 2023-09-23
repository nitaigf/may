# Use a imagem de desenvolvimento Rust para compilar o projeto Yew
FROM ekidd/rust-musl-builder AS builder

# Define o diretório de trabalho
WORKDIR /app

# Copie o código-fonte do frontend para o diretório de trabalho
COPY . .

# Compile o projeto Yew
RUN cargo build --release --target=x86_64-unknown-linux-musl

# Use uma imagem leve do Alpine Linux para a implantação
FROM alpine:latest

# Instale as dependências necessárias (como OpenSSL)
RUN apk --no-cache add ca-certificates

# Copie o executável compilado do projeto Yew da etapa anterior
COPY --from=builder /app/target/x86_64-unknown-linux-musl/release/may_front /app/may_front

# Defina o diretório de trabalho
WORKDIR /app

# Exponha a porta que o servidor Yew usará (ajuste conforme necessário)
EXPOSE 8080

# Execute o aplicativo Yew
CMD ["./may_front"]

