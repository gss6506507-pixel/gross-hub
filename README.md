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

-- Aplicar mudanças
lvlTXT.Text = "Level: " .. novoLevel
dinheiro.Text = "Dinheiro: " .. formatarDinheiro(novoDinheiro)
banco.Text = "Banco: " .. formatarDinheiro(novoBanco)

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
	end
end)
