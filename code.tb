module fir_filter_tb;
    parameter DATA_WIDTH = 16;
    parameter N = 4;

    reg clk;
    reg rst;
    reg signed [DATA_WIDTH-1:0] data_in;
    wire signed [DATA_WIDTH-1:0] data_out;

    // Instantiate the FIR filter
    fir_filter #(N, DATA_WIDTH) uut (
        .clk(clk),
        .rst(rst),
        .data_in(data_in),
        .data_out(data_out)
    );

    // Clock generation
    always #5 clk = ~clk;

    initial begin
        // Initialize signals
        clk = 0;
        rst = 1;
        data_in = 0;

        // Release reset
        #10 rst = 0;

        // Apply test data
        #10 data_in = 16'h000A;
        #10 data_in = 16'h000B;
        #10 data_in = 16'h000C;
        #10 data_in = 16'h000D;
        #10 data_in = 16'h000E;

        // Hold input steady
        #50 data_in = 16'h0000;

        // End simulation
        #100 $finish;
    end

    initial begin
        $monitor("Time = %0t | data_in = %0d | data_out = %0d", $time, data_in, data_out);
    end
endmodule
