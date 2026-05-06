`timescale 1ns / 1ps



module fifo_sync_tb();
    reg clk;
    reg rst;
    reg [7:0]din;
    reg wr_en;
    reg rd_en;
    wire [7:0]dout;
    wire full;
    wire empty;
   
fifo_sync #(
            .WIDTH(8),
            .DEPTH(16)
        ) dut (
            .clk   (clk),
            .rst   (rst),
            .din   (din),
            .wr_en (wr_en),
            .rd_en (rd_en),
            .dout  (dout),
            .full  (full),
            .empty (empty)
        );

    always #5 clk=~clk;
    initial begin   
        clk = 0;
        rst = 1;
        wr_en =0;
        rd_en = 0;
        din = 0;
        @(posedge clk);
                @(posedge clk);
                rst = 0;
        
                // --------------------------------
                // WRITE A1, B2, C3, D4
                // --------------------------------
                @(posedge clk); wr_en = 1; din = 8'hA1;
                @(posedge clk);            din = 8'hB2;
                @(posedge clk);            din = 8'hC3;
                @(posedge clk);            din = 8'hD4;
                @(posedge clk); wr_en = 0;
        
                // --------------------------------
                // READ and CHECK
                // --------------------------------
                @(posedge clk); rd_en = 1;
        
                @(posedge clk);
                $display("Write: A1 | Read: %h | %s", dout, (dout == 8'hA1) ? "PASS" : "FAIL");
        
                @(posedge clk);
                $display("Write: B2 | Read: %h | %s", dout, (dout == 8'hB2) ? "PASS" : "FAIL");
        
                @(posedge clk);
                $display("Write: C3 | Read: %h | %s", dout, (dout == 8'hC3) ? "PASS" : "FAIL");
        
                @(posedge clk);
                $display("Write: D4 | Read: %h | %s", dout, (dout == 8'hD4) ? "PASS" : "FAIL");
        
                @(posedge clk); rd_en = 0;
        
                #20 $finish;
            end
        
        endmodule