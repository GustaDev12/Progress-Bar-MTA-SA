# Progress-Bar-MTA-SA
Sistema de progress bar

Autor:  @Guh#1074 
Descrição: Sistema de progress bar

```lua
local _progress = { }

function CreateProgressBar ( x, y, w, h, speed, colorBackground, colorProgress )

    local self = setmetatable({}, {__index = _progress})

    self.constructor = function ( )

        self.x = x;
        self.y = y;
        self.w = w;
        self.h = h;
        self.speed = speed;
        self.tick = getTickCount ( );
        self.progress = 0;
        self.progressCount = 0;
        self.colorBackground = colorBackground;
        self.colorProgress = colorProgress;

    end;


    self.createProgress = function ( self )

        self.render = function ( )
        
            if self then 

                self.progress_animation = interpolateBetween ( 0, 0, 0, self.w, 0, 0, ( getTickCount ( ) - self.tick ) / tonumber(speed), "Linear" )
                self.progressCount = ( self.progress_animation / self.w * 100 )
    
                dxDrawRectangle(self.x, self.y, self.w, self.h, self.colorBackground)
                dxDrawRectangle(self.x, self.y, self.progress_animation, self.h, self.colorProgress)
                
                dxDrawText("Progresso:"..math.floor(math.ceil(self.progressCount)).."%", self.x + 150, self.y+22  , self.w, self.h, tocolor(255, 255, 255, 255), 1, "Default-bold", "left", "top")

                if ( self.progress_animation == self.w ) then 
                
                    self:destroyProgress ( )
                
                end;

            end;

        end

        addEventHandler("onClientRender", root, self.render)

    end;

    self.destroyProgress = function ( self )

        if self then 

            removeEventHandler("onClientRender", root, self.render)
            self = nil

        end;

    end;

    self.getProgress = function ( self )

        if self then 

            return math.floor(math.ceil(self.progressCount))

        end;

    end;

    self.constructor()

    return self
end;

local progressBar = CreateProgressBar ( 765, 953, 390, 63, 1000, tocolor(47, 47, 47, 255), tocolor(63, 188, 181, 255 ) )

progressBar:createProgress()

--[[

    progressBar:createProgress ( ) | Cria a progress bar
    progressBar:destroyProgress ( ) Destroi a progress bar
    progressBar:getProgress ( ) | Verifica quantos % a progress bar esta

]]

```
