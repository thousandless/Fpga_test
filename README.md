# Fpga_test
----------------------------------------------------------------------------------
-- Company: 
-- Engineer: 
-- 
-- Create Date:    15:53:56 07/03/2025 
-- Design Name: 
-- Module Name:    light - Behavioral 
-- Project Name: 
-- Target Devices: 
-- Tool versions: 
-- Description: 
--
-- Dependencies: 
--
-- Revision: 
-- Revision 0.01 - File Created
-- Additional Comments: 
--
----------------------------------------------------------------------------------
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity light is
    Port ( clk : in  STD_LOGIC;
           rst : in  STD_LOGIC;
			  input : in STD_LOGIC;
			  led : out STD_LOGIC );
end light;

architecture Behavioral of light is

type state_type is (off,A1,A2,A3,A4,A5,A6,B1,B2,B3,B4,C1,C2,C3,C4,C5,C6,D1,D2,D3,D4,E1,E2,E3,E4,E5,E6);
signal nowstate, next_state : state_type;
signal start : std_logic;

begin

SYNC_PROC : process (clk,rst)
begin 
			if (rst = '0') then
					nowstate <= off;
			elsif (rising_edge(clk)) then
					nowstate <= next_state;
			end if;
end process;

NEXT_STATE_DECODE : process (nowstate,input)
begin
	case (nowstate) is 
		when Off =>
			if (input = '0') then
				next_state <= A1;
			else
				next_state <= off;
			end if;
		when A1 	=> next_state <= A2;
		when A2 	=> next_state <= A3;
		when A3 	=> next_state <= A4;
		when A4 	=> next_state <= A5;
		when A5 	=> next_state <= A6;
		when A6 	=> next_state <= B1;
		when B1	=> next_state <= B2;
		when B2 	=> next_state <= B3;
		when B3 	=> next_state <= B4;
		when B4 	=> next_state <= C1;
		when C1 	=> next_state <= C2;
		when C2 	=> next_state <= C3;
		when C3 	=> next_state <= C4;
		when C4 	=> next_state <= C5;
		when C5 	=> next_state <= C6;
		when C6 	=> next_state <= D1;
		when D1 	=> next_state <= D2;					
		when D2 	=> next_state <= D3;
		when D3 	=> next_state <= D4;
		when D4 	=> next_state <= E1;
		when E1 	=> next_state <= E2;
		when E2 	=> next_state <= E3;
		when E3 	=> next_state <= E4;
		when E4 	=> next_state <= E5;
		when E5 	=> next_state <= E6;
		when E6 	=> next_state <= off;
		when others => next_state <= off;
	end case;
end process ;

LED_OUTPUT : process (nowstate,start)
begin
	case (nowstate) is
		when off => led <= '0' ;
		when A1 => led <= '1' ;
		when A2 => led <= '1' ;
		when A3 => led <= '1' ;
		when A4 => led <= '1' ;
		when A5 => led <= '1' ;
		when A6 => led <= '1' ;
		when B1 => led <= '0' ;
		when B2 => led <= '0' ;
		when B3 => led <= '0' ;
		when B4 => led <= '0' ;
		when C1 => led <= '1' ;
		when C2 => led <= '1' ;
		when C3 => led <= '1' ;
		when C4 => led <= '1' ;
		when C5 => led <= '1' ;
		when C6 => led <= '1' ;
		when D1 => led <= '0' ;
		when D2 => led <= '0' ;
		when D3 => led <= '0' ;
		when D4 => led <= '0' ;
		when others => led <= '0';
	end case;
end process;
			
end Behavioral;

