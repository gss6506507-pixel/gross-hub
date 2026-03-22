-- Script Local para Roblox
-- Coloque em StarterGui ou StarterPlayerScripts

local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Aguardar a GUI carregar
local playerGui = player:WaitForChild("PlayerGui")
local backpackNova = playerGui:WaitForChild("BackpackNova")
local metaLIXO = backpackNova:WaitForChild("metaLIXO")

-- Aguardar os elementos específicos
local levelFrame = metaLIXO:WaitForChild("LevelFrame")
local lvlTXT = levelFrame:WaitForChild("LvlTXT")
local expTXT = levelFrame:WaitForChild("ExpTXT")
local tanto = levelFrame:WaitForChild("Tanto")

local values = metaLIXO:WaitForChild("values")
local valoresSalvados = values:WaitForChild("ValoresSalvados")
local dinheiro = valoresSalvados:WaitForChild("Dinheiro")
local banco = valoresSalvados:WaitForChild("Banco")

-- Função para formatar número com separador de milhares
local function formatarDinheiro(valor)
	local formatado = tostring(valor)
	local k
	while true do
		formatado, k = string.gsub(formatado, "^(-?%d+)(%d%d%d)", '%1.%2')
		if k == 0 then
			break
		end
	end
	return "R$ " .. formatado
end

-- Definir valores
local novoLevel = 8
local novoDinheiro = 6247893 -- 6 milhões e alguns quebrados
local novoBanco = 2384761 -- 2 milhões e alguns quebrados
local expAtual = 40
local expMaximo = 700

-- Aplicar mudanças
lvlTXT.Text = "Level: " .. novoLevel
dinheiro.Text = "Dinheiro: " .. formatarDinheiro(novoDinheiro)
banco.Text = "Banco: " .. formatarDinheiro(novoBanco)
expTXT.Text = "Exp: " .. expAtual .. "/" .. expMaximo

-- Ajustar barra de XP
tanto.Size = UDim2.new(0.0871428549, 0, 1, 0)

-- Manter os valores atualizados (caso o jogo tente resetar)
spawn(function()
	while wait(1) do
		if lvlTXT.Text ~= "Level: " .. novoLevel then
			lvlTXT.Text = "Level: " .. novoLevel
		end
		
		local dinheiroFormatado = "Dinheiro: " .. formatarDinheiro(novoDinheiro)
		if dinheiro.Text ~= dinheiroFormatado then
			dinheiro.Text = dinheiroFormatado
		end
		
		local bancoFormatado = "Banco: " .. formatarDinheiro(novoBanco)
		if banco.Text ~= bancoFormatado then
			banco.Text = bancoFormatado
		end
		
		local expTexto = "Exp: " .. expAtual .. "/" .. expMaximo
		if expTXT.Text ~= expTexto then
			expTXT.Text = expTexto
		end
		
		-- Manter o tamanho da barra de XP
		if tanto.Size ~= UDim2.new(0.0871428549, 0, 1, 0) then
			tanto.Size = UDim2.new(0.0871428549, 0, 1, 0)
		end
	end
end)
