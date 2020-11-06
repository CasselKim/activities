# 2 to 1 MUX를 만드는 7가지 방법

# 0. Test bench

```verilog
module MUX_2to1_tb();
	wire y;
	reg a,b,sel;
	
	MUX_2to1 u1(a,b,sel,y);
	
	initial begin
		a=0; b=0; sel=0;
	end
	
	always
		#1 a=~a;
	always
		#2 b=~b;
	always
		#4 sel=~sel;

endmodule
```

# 1. Primitive gates(내장 게이트)

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output y;
	
	wire a0, a1, sn;
	
	not u1 (sn, sel);
	and u2 (a0, a, sn);
	and u3 (a1, b, sel);
	or  u4 (y, a0, a1);
	
endmodule
```

# 2. Not using INV

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output y;
	
	wire a0, a1;
	
	and u2 (a0, a, ~sel);
	and u3 (a1, b, sel);
	or  u4 (y, a0, a1);
	
endmodule
```

# 3. Using only one AND

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output y;
	
	wire a0, a1;
	
	and u2 (a0, a, ~sel), u3 (a1, b, sel);
	or  u4 (y, a0, a1);
	
endmodule
```

# 4. Using `assign` statement

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output y;
	
	assign y = (a&~sel) | (b&sel);
	
endmodule
```

# 5. Using ternary operator ( a ? b : c )

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output y;
	
	// if sel is True -> b , False -> a
	assign y = sel? b : a;
	
endmodule
```

# 6. If/else statement

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	// output으로 reg를 넣어줘야함!!!
	output reg y;
	
	// @(at) (*)(아무대서나)
	always @(*) begin
		if(sel)
			y = b;
		else
			y = a;
	end
	
endmodule
```

# 7. Case statement

```verilog
module MUX_2to1(a,b,sel,y);
	
	input a, b, sel;
	output reg y;
	
	always @(*) begin
		case (sel)
			1'b0 : y = a;
			1'b1 : y = b;
		endcase
	end
	
endmodule
```