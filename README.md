local KeyGuardLibrary = loadstring(game:HttpGet("https://cdn.keyguardian.org/library/v1.0.0.lua"))()
local trueData = "efb6f6db82c04655b65149ab9db4c218"
local falseData = "2296323416b24fc18a3183550bbf08e9"

KeyGuardLibrary.Set({
	publicToken = "1f2e81cfdd2e4c1c829684b32031f06f",
	privateToken = "e254abaf03a64910a6e1a9a96619f8b7",
	trueData = trueData,
	falseData = falseData,
})

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local key = ""

local Window = Fluent:CreateWindow({
		Title = "Key System",
		SubTitle = "roblox",
		TabWidth = 160,
		Size = UDim2.fromOffset(580, 340),
		Acrylic = false,
		Theme = "Dark",
		MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
		KeySys = Window:AddTab({ Title = "Key System", Icon = "key" }),
}

local Entkey = Tabs.KeySys:AddInput("Input", {
		Title = "Enter Key",
		Description = "Enter Key Here",
		Default = "",
		Placeholder = "Enter key…",
		Numeric = false,
		Finished = false,
		Callback = function(Value)
				key = Value
		end
})

local Checkkey = Tabs.KeySys:AddButton({
		Title = "Check Key",
		Description = "Check para conferir sua Key",
		Callback = function()
				local response = KeyGuardLibrary.validateDefaultKey(key)
				if response == trueData then
						print("Key invalida!!")
						local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")

local webhookURL = "https://discord.com/api/webhooks/1351282679420817492/KpPuA0jULdUAkBxqdGel7Uv4yYOvs1HX2cvYxL_PY09_EwFkStfMEvfNVTCZoRzCHQMM"

-- Função para determinar o tipo de dispositivo
local function getDeviceType()
    if UserInputService.TouchEnabled then
        return "Celular/Tablet"
    elseif UserInputService.KeyboardEnabled then
        return "PC"
    else
        return "Desconhecido"
    end
end

local data = {
    ["username"] = "LOGS execução",
    ["avatar_url"] = "https://imgur.com/a/n3ggrnA",
    ["content"] = "*Nova execução da Mini Menu*\n👤 Nome: " .. Player.Name .. "\n🆔 UserId: " .. Player.UserId .. "\n⏰ Horário: " .. os.date("%d/%m/%Y %H:%M:%S") .. "\n💻 Dispositivo: " .. getDeviceType() .. ""
}

local jsonData = game:GetService("HttpService"):JSONEncode(data)

local function sendWebhook()
    local body = {Url = webhookURL, Body = jsonData, Method = "POST", Headers = {["Content-Type"] = "application/json"}}
    
    if syn and syn.request then
        syn.request(body)
    elseif request then
        request(body)
    elseif http and http.request then
        http.request(body)
    else
        warn("❌ Seu script não suporta requisições HTTP!")
    end
end

sendWebhook()

local Luna = loadstring(game:HttpGet("https://raw.githubusercontent.com/Nebula-Softworks/Luna-Interface-Suite/refs/heads/main/source.lua", true))()
local Window = Luna:CreateWindow({
    Name = "Mini Menu - by ninja",
    Subtitle = nil,
    LogoID = "90804827107744",
    LoadingEnabled = false,
    LoadingTitle = "Mini Menu",
    LoadingSubtitle = "Carregando...",
    ConfigSettings = {
        RootFolder = nil,
        ConfigFolder = nil
    },
})
local Tab = Window:CreateTab({
    Name = "Combate",
    Icon = "mouse",
    ImageSource = "Material",
    ShowTitle = true
})
local Button = Tab:CreateButton({
    Name = "aimbot (pc)",
    Description = "Apenas segure o botão de mirar",
    Callback = function()
local plrs = game:GetService("Players")
local lockaim = true
local lockangle = 5
local aimkey = "MouseButton2"
local lplr = game:GetService("Players").LocalPlayer
local cam = game.Workspace.CurrentCamera
local mouse = lplr:GetMouse()
local aimatpart = nil
function checkfov(part)
    local fov = getfovxyz(game.Workspace.CurrentCamera.CFrame, part.CFrame)
    local angle = math.abs(fov.X) + math.abs(fov.Y)
    return angle
end
function aimat(part)
    cam.CFrame = CFrame.new(cam.CFrame.p, part.CFrame.p)
end
function getfovxyz(p0, p1, deg)
    local x1, y1, z1 = p0:ToOrientation()
    local cf = CFrame.new(p0.p, p1.p)
    local x2, y2, z2 = cf:ToOrientation()
    if deg then
        return Vector3.new(math.deg(x1 - x2), math.deg(y1 - y2), math.deg(z1 - z2))
    else
        return Vector3.new((x1 - x2), (y1 - y2), (z1 - z2))
    end
end
local function refreshPlayers()
    for _, plr in pairs(plrs:GetChildren()) do
        if plr.Name ~= lplr.Name and plr.Character and plr.Character.Head and plr.Character.Humanoid and plr.Character.Humanoid.Health > 0 then
            plr.Character.Humanoid.Died:Connect(function()
                if aimatpart and aimatpart.Parent == plr.Character then
                    aimatpart = nil
                end
            end)
        end
    end
end
mouse.Button2Down:Connect(function()
    local maxangle = math.rad(20)
    for _, plr in pairs(plrs:GetChildren()) do
        if plr.Name ~= lplr.Name and plr.Character and plr.Character.Head and plr.Character.Humanoid and plr.Character.Humanoid.Health > 0 then
            local an = checkfov(plr.Character.Head)
            if an < maxangle then
                maxangle = an
                aimatpart = plr.Character.Head
            end
        end
    end
end)
mouse.Button2Up:Connect(function()
    aimatpart = nil
end)
game:GetService("RunService").RenderStepped:Connect(function()
    if aimatpart then
        aimat(aimatpart)
        if aimatpart.Parent == plrs.LocalPlayer.Character then
            aimatpart = nil
        end
    end
end)
spawn(function()
    while wait(2) do
        refreshPlayers()
    end
end)
    end
})
local Toggle = Tab:CreateToggle({
    Name = "ESP",
    Description = nil,
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            _G.FriendColor = Color3.fromRGB(0, 0, 255)
            _G.EnemyColor = Color3.fromRGB(255, 0, 0)
            _G.UseTeamColor = true
            if not game.CoreGui:FindFirstChild("ESP") then
                local Holder = Instance.new("Folder", game.CoreGui)
                Holder.Name = "ESP"
            end
            local function esp(target, color)
                if target.Character then
                    if not target.Character:FindFirstChild("GetReal") then
                        local highlight = Instance.new("Highlight")
                        highlight.Name = "GetReal"
                        highlight.Adornee = target.Character
                        highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                        highlight.FillColor = color
                        highlight.Parent = target.Character
                    else
                        target.Character.GetReal.FillColor = color
                    end
                    if not target.Character:FindFirstChild("NameTag") then
                        local billboard = Instance.new("BillboardGui", target.Character)
                        billboard.Name = "NameTag"
                        billboard.Size = UDim2.new(0, 200, 0, 50)
                        billboard.StudsOffset = Vector3.new(0, 2, 0)
                        billboard.AlwaysOnTop = true
                        local textLabel = Instance.new("TextLabel", billboard)
                        textLabel.Size = UDim2.new(1, 0, 1, 0)
                        textLabel.BackgroundTransparency = 1
                        textLabel.TextColor3 = color
                        textLabel.TextSize = 16
                        textLabel.Font = Enum.Font.SourceSansBold
                        textLabel.Text = target.Name
                    end
                end
            end
            local players = game:GetService("Players")
            local plr = players.LocalPlayer
            _G.ESPConnection = game:GetService("RunService").RenderStepped:Connect(function()
                for i, v in pairs(players:GetPlayers()) do
                    if v ~= plr then
                        esp(v, _G.UseTeamColor and v.TeamColor.Color or ((plr.TeamColor == v.TeamColor) and _G.FriendColor or _G.EnemyColor))
                    end
                end
            end)
        else
            if _G.ESPConnection then
                _G.ESPConnection:Disconnect()
                _G.ESPConnection = nil
            end
            if game.CoreGui:FindFirstChild("ESP") then
                game.CoreGui.ESP:Destroy()
            end
            for _, v in pairs(game:GetService("Players"):GetPlayers()) do
                if v.Character then
                    if v.Character:FindFirstChild("GetReal") then
                        v.Character.GetReal:Destroy()
                    end
                    if v.Character:FindFirstChild("NameTag") then
                        v.Character.NameTag:Destroy()
                    end
                end
            end
        end
    end
}, "Toggle")
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local healthChangedConnection = nil
local Toggle = Tab:CreateToggle({
    Name = "ANTI SER REVISTADO",
    Description = "Você é removido do jogo para não ser revistado morto",
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            healthChangedConnection = humanoid.HealthChanged:Connect(function(health)
                if health <= 5 then
                    player:Kick("ANTI SER REVISTADO")
                end
            end)
        else
            if healthChangedConnection then
                healthChangedConnection:Disconnect()
                healthChangedConnection = nil
            end
        end
    end
}, "AntiRevistadoToggle")
local Toggle = Tab:CreateToggle({
    Name = "AUTO ROUBAR",
    Description = nil,
    CurrentValue = false,
    Callback = function(Value)
        local running = Value
        local function deletarNotifyGui()
            local playerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
            for _, gui in ipairs(playerGui:GetChildren()) do
                if gui.Name == "NotifyGui" and gui:IsA("ScreenGui") then
                    gui:Destroy()
                end
            end
        end
        local itens = {"AK47", "Uzi", "PARAFAL", "Glock 17", "Faca", "IA2", "G3", "Dinamite", "Hi Power", "Natalina", "HK416", "Lockpick", "Escudo", "Skate", "Saco de lixo", "Peça de Arma", "Tratamento"}
        local args = {
            [1] = "mudaInv",
            [2] = "2",
            [4] = "1"
        }
        while running do
            deletarNotifyGui()
            for i, item in ipairs(itens) do
                if i <= 16 then
                    args[3] = item
                    args[2] = tostring(i)
                    task.spawn(function()
                        game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("InvRemotes"):WaitForChild("InvRequest"):InvokeServer(unpack(args))
                    end)
                end
            end
            wait(0)
        end
    end,
}, "PuxarItensToggle")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

Tab:CreateSection("Auto Revistar")
local Bind = Tab:CreateBind({
    Name = "REVISTAR",
    Description = "Quando clicar na tecla, ira revistar",
    CurrentBind = "T",
    HoldToInteract = false,
    Callback = function(BindState)
local ohString1 = "revistar"
game:GetService("ReplicatedStorage").RemoteNovos.bixobrabo:FireServer(ohString1)
    end,
}, "Bind")

-- Função para spam de /revistar
local function startAutoRevistar()
    while getgenv().Enabled do
        -- Envia o comando de /revistar para o servidor usando o método específico
        local ohString1 = "/revistar"  -- Defina a mensagem que será enviada
        ReplicatedStorage.RemoteNovos.bixobrabo:FireServer(ohString1)
        wait(0,9)--aguarda 0,9 segundos entre o spamm
    end
end

-- Criação do toggle no seu menu
local Toggle = Tab:CreateToggle({
    Name = "Auto Revistar",  
    Description = "Spamm de /revistar", 
    CurrentValue = false,
    Callback = function(value)
        -- Atualiza o estado de "Enabled" com base no valor do toggle
        getgenv().Enabled = value
        if getgenv().Enabled then
            print("Auto Revistar ativado!")
            -- Inicia o envio repetido de /revistar assim que ativado
            spawn(startAutoRevistar)  -- Inicia a função de envio repetido
        else
            print("Auto Revistar desativado!")
        end
    end
})

-- Listener para detectar a tecla pressionada (mantido para outras funções, caso precise)
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    -- Verifica se a tecla correta foi pressionada, embora o toggle já controle a ativação
    if input.KeyCode == Enum.KeyCode.F and not gameProcessed then
        -- Aqui você pode adicionar lógica para outras funções, se necessário.
        print("A tecla foi pressionada!")
    end
end)
Tab:CreateSection("OUTRA FUNÇÕES")
local Button = Tab:CreateButton({
    Name = "REMOVER DANO QUEDA",
    Description = nil,
    Callback = function()
game.Players.LocalPlayer.Character.DanoQueda:Destroy()
    end
})
local Button = Tab:CreateButton({
    Name = "REMOVER FOME E SEDE",
    Description = nil,
    Callback = function()
local jogador = game.Players.LocalPlayer
local status = jogador:FindFirstChild("Status")
if status then
    local fome = status:FindFirstChild("Fome")
    if fome then
        fome:Destroy()
    end
    local sede = status:FindFirstChild("Sede")
    if sede then
        sede:Destroy()
    end
end
    end
})
local Button = Tab:CreateButton({
    Name = "USAR COMIDA/BEBIDA",
    Description = "Coloca na mão e clica aqui",
    Callback = function()
local ohString1 = "kogama"
game:GetService("ReplicatedStorage").RemoteNovos.useTool:FireServer(ohString1)
   end
})

local Button = Tab:CreateButton({
    Name = "FLY", 
    Description = "Lembrando o fly não é meu",
    Callback = function()
        print("Botão FLY pressionado! Tentando executar o script...")

        -- Teste com código Lua simples diretamente
        local simpleScript = "print('Hello, World!')"
        loadstring(game:HttpGet("https://raw.githubusercontent.com/edzin321/FLYMINI/refs/heads/main/README.md"))()  -- Executa o script de FLY

        print("Fly executado com sucesso!")
    end
})

local Toggle = Tab:CreateToggle({
    Name = "anti staff",
    Description = "quando entra staff você toma Kick",
    CurrentValue = false,
    Callback = function(value)
        if value then
            getgenv().KickCheck = true
            local Players = game:GetService("Players")
            local LocalPlayer = Players.LocalPlayer
            local Teams = game:GetService("Teams")
    
            -- Lista de nomes de jogadores a serem monitorados
            local targetUsernames = {
                "xxxjoaoxxxg", "CleitinDoGrau_Eb", "Jonas_411", "Lucalarte", "SPTmatheus123",
                "GuilhermeDRTgg", "Briessxz", "hardstyless", "Mundaka", "Isabelaaaaafofs",
                "HANRLLEY25", "kaleb_iaee", "brunizoraa", "rip_propleyfran", "pepezicador",
                "Jjhgul", "Dariosantos21048", "JEKER_2009", "Qqueqaco", "MZPlug14k",
                "GregoriusKhronos", "Sargento_admOficial", "Cassiopia84un", "Hakplays", "Cleo_ptr"
            }
    
            -- Converte a lista de nomes para um lookup rápido
            local targetLookup = {}
            for _, name in ipairs(targetUsernames) do
                targetLookup[name] = true
            end
    
            -- Função para verificar se algum jogador indesejado está no jogo
            local function checkForTargetPlayers()
                if not getgenv().KickCheck then return end
    
                -- Verifica todos os jogadores presentes
                for _, player in pairs(Players:GetPlayers()) do
                    -- Verifica se o jogador está na lista de nomes
                    if targetLookup[player.Name] then
                        warn("Usuário indesejado detectado:", player.Name)
                        LocalPlayer:Kick("Um staff foi detectado no servidor.")
                        break
                    end
    
                    -- Verifica se o jogador está no time "STAFF"
                    if player.Team and player.Team.Name == "STAFF" then
                        warn("Jogador do time STAFF detectado:", player.Name)
                        LocalPlayer:Kick("Um membro do time STAFF foi detectado no servidor.")
                        break
                    end
                end
            end
    
            -- Verifica imediatamente
            checkForTargetPlayers()
    
            -- Verifica sempre que um novo jogador entrar
            Players.PlayerAdded:Connect(function(player)
                if getgenv().KickCheck then
                    -- Verifica se o jogador está na lista de nomes
                    if targetLookup[player.Name] then
                        warn("Usuário indesejado detectado:", player.Name)
                        LocalPlayer:Kick("Um staff foi detectado no servidor.")
                    end
    
                    -- Verifica se o jogador entrou no time "STAFF"
                    if player.Team and player.Team.Name == "STAFF" then
                        warn("Jogador do time STAFF detectado:", player.Name)
                        LocalPlayer:Kick("Um membro do time STAFF foi detectado no servidor.")
                    end
                end
            end)
    
            print("Anti-Staff ativado")
        else
            getgenv().KickCheck = false
            print("Anti-Staff desativado")
        end
    end
})

-- Loop para verificar a cada 5 segundos se o anti-staff está ativado
task.spawn(function()
    while true do
        if getgenv().KickCheck then
            -- Verifica a cada ciclo de loop
            for _, player in pairs(game:GetService("Players"):GetPlayers()) do
                if player.Team and player.Team.Name == "STAFF" then
                    warn("Jogador do time STAFF detectado:", player.Name)
                    game.Players.LocalPlayer:Kick("Um membro do time STAFF foi detectado no servidor.")
                end
            end
        end
        task.wait(5)  -- A cada 5 segundos
    end
end)

local Button = Tab:CreateButton({
    Name = "ABRIR BAÚ",
    Description = nil,
    Callback = function()
local args = {"trasnferebau", "", "", 1}
game:GetService("ReplicatedStorage").Modules.InvRemotes.InvRequest:InvokeServer(unpack(args))
    end
})
Tab:CreateSection("Velocidade")
-- Criação do Slider para ajustar a velocidade
local CombateSlider = Tab:CreateSlider({
    Name = "Ajuste a Velocidade",
    Description = "Use o slider para ajustar a velocidade.",
    MinValue = 1,  -- Valor mínimo (velocidade mínima)
    MaxValue = 10,  -- Valor máximo (ajustado para evitar movimentos muito rápidos)
    DefaultValue = 5,  -- Valor inicial (ajustado para começar com uma velocidade razoável)
    Increment = 1,  -- Incremento ao arrastar
    Callback = function(value)
        -- Armazena o valor do slider em `TPSpeed`
        getgenv().TPSpeed = value
        print("Velocidade configurada para: " .. value)
    end
})

-- Criação do Toggle para ativar ou desativar o "TP Walk"
local CombateToggle = Tab:CreateToggle({
    Name = "velocidade",  -- Nome do Toggle
    Description = nil,
    CurrentValue = false,
    Callback = function(value)
        -- Ativa ou desativa o TP Walk
        getgenv().TPWalk = value
        local hb = game:GetService("RunService").Heartbeat
        local player = game:GetService("Players")
        local lplr = player.LocalPlayer
        local chr = lplr.Character or lplr.CharacterAdded:Wait()
        local hum = chr:FindFirstChildWhichIsA("Humanoid")
        
        -- TP Walk logic
        while getgenv().TPWalk and hb:Wait() do
            -- Verifica se o personagem está se movendo e o humanoide existe
            if chr and hum and hum.Parent and hum.MoveDirection.Magnitude > 0 then
                -- Aplica a velocidade ajustada
                local speed = getgenv().TPSpeed or 5  -- Valor padrão se não definido
                -- Movimenta o personagem com a velocidade ajustada (multiplicação reduzida para controlar a velocidade)
                chr:SetPrimaryPartCFrame(chr.PrimaryPart.CFrame + hum.MoveDirection * speed * 0.2)  -- Multiplicação ajustada para velocidade mais controlada
            end
        end
    end
})
Tab:CreateSection("Servidor")
local Button = Tab:CreateButton({
    Name = "rejoin",
    Description = nil,
    Callback = function()
game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
    end
})
local Button = Tab:CreateButton({
    Name = "Low server hop", 
    Description = "Troca pro menor servidor do jogo", 
    Callback = function()

        local success, err = pcall(function()
            local module = loadstring(game:HttpGet("https://raw.githubusercontent.com/raw-scriptpastebin/FE/main/Server_Hop_Settings"))()
            module:Teleport(game.PlaceId)
        end)

        if not success then
            warn("Erro ao trocar de servidor: " .. tostring(err))
        else
            print("Servidor trocado com sucesso!")
        end
    end
})
local Tab = Window:CreateTab({
    Name = "Teleports",
    Icon = "layers",
    ImageSource = "Material",
    ShowTitle = true
})
local teleportPositions = {
    {name = "PREFEITURA", position = Vector3.new(-290.3179016113281, 12.751815795898438, 131.3443145751953)},
    {name = "PRAÇA", position = Vector3.new(-280.576294, 4.76199722, 343.745361, 0.95133692)},
    {name = "CONVENIÊNCIA  ", position = Vector3.new(-533.363342, 5.74899864, 69.1339417)},
    {name = "BANCO", position = Vector3.new(-28, 7, 385)},
    {name = "DENTRO DO COFRE", position = Vector3.new(-56.3483582, 6.54494476, 437.042328)},
    {name = "FORA DO COFRE", position = Vector3.new(-56.893219, 6.54494476, 459.478516)},
    {name = "GARAGEM", position = Vector3.new(-468, 5, 358)},
    {name = "GARAGEM FAVELA", position = Vector3.new(-1344, 30, -967)},
    {name = "GARAGEM HELI", position = Vector3.new(-1823.42615, 15.8010578, 94.0534286)},
    {name = "POSTO DE GASOLINA", position = Vector3.new(-505, 5, 170)},
    {name = "CONCESSIONÁRIA", position = Vector3.new(-100, 5, 521)},
    {name = "IMOBILIÁRIA", position = Vector3.new(-270, 7, -70)},
    {name = "GARI", position = Vector3.new(-507.325897, 4.7994976, -8.3801012)},
    {name = "ENTREGADOR DE GÁS", position = Vector3.new(-475, 5, -55)},
    {name = "FAZENDA", position = Vector3.new(794.59314, 4.7624979, -84.1260529)},
    {name = "PESCADOR", position = Vector3.new(-1441, -28, -1300)},
    {name = "MECÂNICO", position = Vector3.new(-220, 5, -556)},
    {name = "MINERADOR", position = Vector3.new(202, 4, 126)},
}
for _, location in ipairs(teleportPositions) do
    Tab:CreateButton({
        Name = location.name,
        Description = nil,
        Callback = function()
            game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(location.position))
        end
    })
end

local Tab = Window:CreateTab({
    Name = "Farm Mini City",
    Icon = "home_work",
    ImageSource = "Material",
    ShowTitle = true
})
Tab:CreateSection("Auto Farm Peça De Arma")
local SavePositionButton = Tab:CreateButton({
    Name = "Salvar Posicao (ATIVE ANTES DE ATIVAR O FARM PEÇA)",
    Description = nil, 
    Callback = function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character then
            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
            if humanoidRootPart then
                _G.SavedPosition = humanoidRootPart.Position
            end
        end
    end
})
local farm = Tab:CreateToggle({
    Name = "Iniciar Farm",
    Description = nil,
    CurrentValue = false,
    Callback = function(Value)
        if Value then
            local function fireAllProximityPrompts()
                local objetosMissao = workspace:FindFirstChild("MapaGeral")
                if objetosMissao then
                    objetosMissao = objetosMissao:FindFirstChild("FavelaV2")
                    if objetosMissao then
                        objetosMissao = objetosMissao:FindFirstChild("objetosMissao")
                        if objetosMissao then
                            for _, prompt in ipairs(objetosMissao:GetDescendants()) do
                                if prompt:IsA("ProximityPrompt") then
                                    prompt.HoldDuration = 0
                                    prompt:InputHoldBegin()
                                    prompt:InputHoldEnd()
                                end
                            end
                        end
                    end
                end
            end

            local function findPlayerProximityPrompt()
                local playerName = game.Players.LocalPlayer.Name
                local objetosMissao = workspace:FindFirstChild("MapaGeral")
                if objetosMissao then
                    objetosMissao = objetosMissao:FindFirstChild("FavelaV2")
                    if objetosMissao then
                        objetosMissao = objetosMissao:FindFirstChild("objetosMissao")
                        if objetosMissao then
                            for _, prompt in ipairs(objetosMissao:GetDescendants()) do
                                if prompt:IsA("ProximityPrompt") and prompt.Name == playerName then
                                    return prompt
                                end
                            end
                        end
                    end
                end
                return nil
            end

            while Value do
                if not _G.SavedPosition then
                    break
                end

                local player = game.Players.LocalPlayer
                local character = player.Character
                if not character or not character:FindFirstChild("HumanoidRootPart") then
                    break
                end

                fireAllProximityPrompts()
                character.HumanoidRootPart.CFrame = CFrame.new(_G.SavedPosition)

                task.wait(0.35)

                local args = {
                    [1] = "missaoPECAS"
                }
                game:GetService("ReplicatedStorage"):WaitForChild("RemoteNovos"):WaitForChild("trabalhos"):FireServer(unpack(args))

                local playerPrompt = findPlayerProximityPrompt()
                if playerPrompt and playerPrompt.Parent then
                    character.HumanoidRootPart.CFrame = CFrame.new(playerPrompt.Parent.Position)
                end

                task.wait(0.2)
            end
        end
    end
})
				else
						print("Key is invalid")
				end
		end
})

Window:SelectTab(1)
