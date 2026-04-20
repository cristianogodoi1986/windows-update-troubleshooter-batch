# 🔧 Windows Update Fix Toolkit

Script em Batch para reset completo do Windows Update no Windows 10 e 11.

Este projeto automatiza o processo de correção de falhas comuns no Windows Update, limpando cache, reiniciando serviços e forçando nova detecção de atualizações.

---

## 🚀 Problemas que ele resolve

- Windows Update travado
- Erro ao baixar atualizações
- Atualizações não aparecem
- Serviços do Windows Update corrompidos
- Cache de atualização inconsistente

---

## ⚙️ Como funciona

O script executa automaticamente:

1. Parada dos serviços do Windows Update
2. Limpeza do cache (SoftwareDistribution e catroot2)
3. Reinício dos serviços essenciais
4. Força detecção de novas atualizações

---

## 🧰 Serviços afetados

- wuauserv (Windows Update)
- cryptSvc (Serviço de Criptografia)
- bits (Transferência em segundo plano)
- msiserver (Windows Installer)

---

## 📜 Como usar

1. Clique com botão direito no arquivo `.bat`
2. Execute como **Administrador**
3. Aguarde o processo finalizar
4. Reinicie o computador

---

## 💻 Código principal

```bat
@echo off
title CORRECAO WINDOWS UPDATE
color 0E

echo ===============================
echo RESET DO WINDOWS UPDATE
echo ===============================
pause

echo Parando servicos...
net stop wuauserv >nul 2>&1
net stop cryptSvc >nul 2>&1
net stop bits >nul 2>&1
net stop msiserver >nul 2>&1

echo Limpando cache do Windows Update...
ren C:\Windows\SoftwareDistribution SoftwareDistribution.old >nul 2>&1
ren C:\Windows\System32\catroot2 catroot2.old >nul 2>&1

echo Reiniciando servicos...
net start wuauserv >nul 2>&1
net start cryptSvc >nul 2>&1
net start bits >nul 2>&1
net start msiserver >nul 2>&1

echo Forcando deteccao de atualizacoes...
wuauclt /detectnow
wuauclt /reportnow

echo ===============================
echo CONCLUIDO!
echo Reinicie o computador.
echo ===============================
pause
