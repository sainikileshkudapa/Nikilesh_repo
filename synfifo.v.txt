`timescale 1ns / 1ps



module fifo_sync#(

parameter WIDTH = 8,
parameter DEPTH = 16)
(
    input clk,
    input rst,
    input [7:0] din,
    input wr_en,
    input rd_en,
    output reg [7:0] dout,
    output full,
    output empty
    
    );
   reg[7:0] mem[0:15];
   reg [4:0] wr_ptr;
   reg [4:0] rd_ptr;
   
  assign empty= (wr_ptr==rd_ptr);
  assign full = (wr_ptr[3:0]==rd_ptr[3:0])&&(wr_ptr[4]!=rd_ptr[4]);
  
  always @(posedge clk)
  begin 
     if(rst) begin
        wr_ptr <=0;
     end 
     else if(wr_en &&!full)
       begin 
          mem[wr_ptr[3:0]]<= din;
          wr_ptr <= wr_ptr +1;
          end 
      end 
   
   always @(posedge clk)
     begin
      if(rst) begin
         rd_ptr<= 0;
       end
      else if( rd_en && !empty)
       begin 
        dout <= mem[rd_ptr[3:0]];
        rd_ptr <= rd_ptr+1;
        end 
     end

endmodule