library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity ClockMod is
    Port ( clk : in  STD_LOGIC;
           rst : in  STD_LOGIC;
			  Led : out 	STD_LOGIC;
           clockout: out  STD_LOGIC);
end ClockMod;

architecture Behavioral of ClockMod is

	signal tmp : std_logic:='0' ;
	signal div : integer range 0 to 7499999 := 0 ;
	signal WLed : std_logic:='0' ;
	
begin

	
	process (clk,rst,tmp,div,WLed)
	begin
		if (rst='0')then
			tmp <= '0' ;
			div <= 0 ;
			WLed <= '0' ;
		else
			if(rising_edge(clk)) then
				if (div = 7499999 )then
					tmp <= not tmp ;
					div <= 0 ;
					WLed <= tmp;
				else 
					tmp <= tmp ;
					div <= div+1 ;
					
				end if ;
			end if ;
		end if;
	end process ;
					 
	Led <= WLed ;				 
	clockout <= tmp ;


end Behavioral;
