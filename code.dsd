module fir_filter #(parameter N = 4, DATA_WIDTH = 16)(
    input wire clk,
    input wire rst,
    input wire signed [DATA_WIDTH-1:0] data_in,
    output reg signed [DATA_WIDTH-1:0] data_out
);

    // Coefficients of the FIR filter
    reg signed [DATA_WIDTH-1:0] coeffs[N-1:0];

    // Shift register for input samples
    reg signed [DATA_WIDTH-1:0] shift_reg[N-1:0];

    integer i;

    initial begin
        coeffs[0] = 16'h0003;
        coeffs[1] = 16'h0005;
        coeffs[2] = 16'h0007;
        coeffs[3] = 16'h0009;
    end

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            data_out <= 0;
            for (i = 0; i < N; i = i + 1) begin
                shift_reg[i] <= 0;
            end
        end else begin
            // Shift the data through the shift register
            for (i = N-1; i > 0; i = i - 1) begin
                shift_reg[i] <= shift_reg[i-1];
            end
            shift_reg[0] <= data_in;

            // FIR filter convolution
            data_out <= 0;
            for (i = 0; i < N; i = i + 1) begin
                data_out <= data_out + (shift_reg[i] * coeffs[i]);
            end
        end
    end
endmodule
