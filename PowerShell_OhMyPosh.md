# 🧩 **PASSO A PASSO — PowerShell + Oh My Posh no Windows**


- PowerShell moderno (7+)
- Tema Paradox ativo
- Aliases e funções úteis
- Ambiente pronto pra Git, Docker, Node

---

## 🪟 **1️⃣ Instalar o PowerShell moderno (se ainda não tiver)**

O **Oh My Posh** funciona melhor no **PowerShell 7+ (pwsh)**, não no antigo `Windows PowerShell 5.x`.

### ✅ Instalação via Winget

Abra o CMD ou o PowerShell antigo e rode:

```powershell
winget install --id Microsoft.PowerShell -e

```

> 💡 Após instalar, abra o menu iniciar e procure por “PowerShell 7” (ou “PowerShell”) — é esse que você vai usar daqui pra frente.
> 

---

## 🎨 **2️⃣ Instalar o Oh My Posh**

No PowerShell 7, execute:

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget

```

Verifique se foi instalado corretamente:

```powershell
oh-my-posh version

```

Deve aparecer algo como:

```
Oh My Posh version: 24.12.3

```

---

## 🖋️ **3️⃣ Criar o arquivo de perfil do PowerShell**

O perfil é o arquivo que carrega suas configurações sempre que você abre o terminal.

### Verifique se o perfil existe:

```powershell
Test-Path $PROFILE

```

Se retornar **False**, crie ele:

```powershell
New-Item -Path $PROFILE -ItemType File -Force

```

Agora abra:

```powershell
notepad $PROFILE

```

---

## ⚙️ **4️⃣ Configurar o tema do Oh My Posh**

Dentro do arquivo aberto no Notepad, cole:

```powershell
# ===========================
# Perfil PowerShell + Oh My Posh
# ===========================

# Inicializa o Oh My Posh com o tema Paradox
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression

# Personalização do título da janela
$host.UI.RawUI.WindowTitle = "💻 PowerShell - $(Get-Date -Format 'dd/MM/yyyy HH:mm')"

# Alias úteis
Set-Alias ll Get-ChildItem
Set-Alias la "Get-ChildItem -Force"
Set-Alias gs "git status"
Set-Alias gpl "git pull"
Set-Alias gph "git push"
Set-Alias gcom "git commit"
Set-Alias gco "git checkout"
Set-Alias gll "git log --oneline --graph --decorate"
Set-Alias code "code ."
Set-Alias cls Clear-Host

# Função mkcd - cria e entra em uma pasta
function mkcd {
    param([string]$name)
    if (-not $name) {
        Write-Host "Uso: mkcd <nome-da-pasta>" -ForegroundColor Yellow
        return
    }
    New-Item -ItemType Directory -Path $name -ErrorAction SilentlyContinue | Out-Null
    Set-Location $name
}

# Atalhos para pastas comuns
function dev { Set-Location "$HOME\Documents\Projetos" }
function desk { Set-Location "$HOME\Desktop" }
function dl { Set-Location "$HOME\Downloads" }

# Atualizar pacotes do Winget
function update-all {
    Write-Host "🔄 Atualizando pacotes via winget..." -ForegroundColor Cyan
    winget upgrade --all
}

# Mostrar informações do ambiente
function sys-info {
    Write-Host "⚙️  Ambiente de Desenvolvimento" -ForegroundColor Green
    Write-Host "----------------------------------"
    Write-Host "PowerShell: $($PSVersionTable.PSVersion)"
    Write-Host "Node.js: $(node --version 2>$null)"
    Write-Host "npm: $(npm --version 2>$null)"
    Write-Host "Python: $(python --version 2>$null)"
    Write-Host "Docker: $(docker --version 2>$null)"
    Write-Host "Git: $(git --version 2>$null)"
    Write-Host "----------------------------------"
}

Write-Host "✅ Perfil carregado com sucesso!" -ForegroundColor Green
Write-Host "💡 Use 'sys-info' para ver versões, 'update-all' para atualizar tudo."

```

Salve o arquivo e feche o Notepad.

---

## 🔁 **5️⃣ Recarregar o perfil**

Para aplicar sem reiniciar o terminal:

```powershell
. $PROFILE

```

---

## ✨ **6️⃣ Confirmar que o Oh My Posh está funcionando**

Feche e reabra o **PowerShell (7+)**.

Você deve ver o prompt com o tema **Paradox** ativo, colorido e estilizado 🎨

Exemplo visual:

```
 usuario@PC   Projetos   main ↑1   node v20.11.0 
❯

```

---

## 🧱 **7️⃣ (Opcional) — Trocar o tema**

Liste os temas disponíveis:

```powershell
Get-ChildItem $env:POSH_THEMES_PATH

```

Testar outro tema sem editar o perfil:

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\ys.omp.json" | Invoke-Expression

```

Se gostar, troque o nome do tema no `$PROFILE`.

---

## 🧠 **8️⃣ Dicas úteis**

| Comando | O que faz |
| --- | --- |
| `ll` | Lista arquivos |
| `dev` | Vai para a pasta de projetos |
| `mkcd app` | Cria e entra em `app` |
| `gcom -m "mensagem"` | Git commit |
| `update-all` | Atualiza apps via Winget |
| `sys-info` | Mostra versão do Node, Python, etc |

---

## 🧰 **9️⃣ (Opcional) — Ativar PowerShell como padrão no Windows Terminal**

1. Abra o **Windows Terminal**
2. Vá em **Configurações → Perfil padrão → PowerShell**
3. Salve.

Assim, toda nova aba já abrirá com seu PowerShell estilizado com Oh My Posh 😎
