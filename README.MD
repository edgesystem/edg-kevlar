# Edge-Kevlar. 3 Níveis de colete + itens de produção Resource FREE para membros da comunidade https://discord.gg/jCxadac2vt Edge System. 

Este recurso adiciona coletes funcionais ao seu servidor FiveM usando uma única dependência **ox_inventory**.  
Inclui três tipos de colete: **Leve**, **Reforçado** e **Tático**.

---

## Imagens dos Coletes

Coloque as imagens em:  
ox_inventory/web/images

yaml
Copiar código

- `colete_leve.png`  
- `colete_reforcado.png`  
- `colete_tatico.png`  

---

## Configuração dos Coletes

Para que os coletes funcionem, adicione o seguinte em:  

ox_inventory/modules/items/client.lua

**Após a linha 111:**

```lua
Item('colete_leve', function(data, slot)
    if GetPedArmour(cache.ped) < 100 then
        ox_inventory:useItem(data, function(data)
            if data then
                SetPlayerMaxArmour(PlayerData.id, 100)
                SetPedArmour(cache.ped, 25) -- Colete leve: 25% de armadura
            end
        end)
    end
end)

Item('colete_reforcado', function(data, slot)
    if GetPedArmour(cache.ped) < 100 then
        ox_inventory:useItem(data, function(data)
            if data then
                SetPlayerMaxArmour(PlayerData.id, 100)
                SetPedArmour(cache.ped, 50) -- Colete reforçado: 50% de armadura
            end
        end)
    end
end)

Item('colete_tatico', function(data, slot)
    if GetPedArmour(cache.ped) < 100 then
        ox_inventory:useItem(data, function(data)
            if data then
                SetPlayerMaxArmour(PlayerData.id, 100)
                SetPedArmour(cache.ped, 100) -- Colete tático: 100% de armadura
            end
        end)
    end
end)


Item('placa_rapida', function(data, slot)
    local ped = cache.ped
    local currentArmour = GetPedArmour(ped)

    -- Só repara se já existir colete equipado e não estiver completo
    if currentArmour > 0 and currentArmour < 100 then
        ox_inventory:useItem(data, function(success)
            if success then
                local repaired = math.min(currentArmour + 25, 100)
                SetPedArmour(ped, repaired)
            end
        end)
    end
end)



Registro no ox_inventory
Para que os coletes sejam reconhecidos, edite:

ox_inventory/data/items.lua

Coloque os itens em uma posição de sua preferência (ex: linha 414 para baixo):

 ## COLETES 


["colete_leve"] = {
	label = "Colete Leve",
	weight = 3000,
	stack = false,
	client = {
		image = "colete_leve.png",
		anim = { dict = "clothingshirt", clip = "try_shirt_positive_d" },
		usetime = 3500,
	},
},

["colete_reforcado"] = {
	label = "Colete Reforçado",
	weight = 3000,
	stack = false,
	client = {
		image = "colete_reforcado.png",
		anim = { dict = "clothingshirt", clip = "try_shirt_positive_d" },
		usetime = 3500,
	},
},

["colete_tatico"] = {
	label = "Colete Tático",
	weight = 3000,
	stack = false,
	client = {
		image = "colete_tatico.png",
		anim = { dict = "clothingshirt", clip = "try_shirt_positive_d" },
		usetime = 3500,
	},
},
["placa_rapida"] = {
	label = "Placa Rápida",
	weight = 100,
	stack = false,
	client = {
		image = "placa_rapida.png",
		anim = { dict = "clothingshirt", clip = "try_shirt_positive_d" },
		usetime = 1800,
	},
},

## ITEMS DE PRODUCAO
* os items de producao podem ser configurados nas mesas de crafting ligados aos coletes para tornar mais imersivo a producao dos coletes.

["placa_metalica"] = {
	label = "Placa Metálica",
	weight = 500,
	stack = true,
	close = false,
	description = "Placa rígida utilizada na estrutura interna de coletes.",
	client = {
		image = "placa_metalica.png",
	},
},

["tecido_resistente"] = {
	label = "Tecido Resistente",
	weight = 100,
	stack = true,
	close = false,
	description = "Material têxtil reforçado, usado para vestimentas de proteção.",
	client = {
		image = "tecido_resistente.png",
	},
},

["fibra_kevlar"] = {
	label = "Fibra de Kevlar",
	weight = 150,
	stack = true,
	close = false,
	description = "Fibra sintética ultrarresistente para coletes balísticos.",
	client = {
		image = "fibra_kevlar.png",
	},
},



## OBRIGADO POR USAR O NOSSO PACK/SCRIPT. EDGE SYSTEM 2025

Observações
O colete leve dá 25% de armadura.

O colete reforçado dá 50% de armadura.

O colete tático dá 100% de armadura.

Certifique-se de reiniciar o servidor após adicionar os itens para que sejam reconhecidos.

