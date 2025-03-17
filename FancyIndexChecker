def format_number(input_value):
    """Format and print a single number in hexadecimal form with aligned indices."""
    # Convert input to hexadecimal (if not already in hex format)
    if isinstance(input_value, int):
        hex_str = hex(input_value)[2:].upper()
    else:
        hex_str = input_value.replace(" ", "").upper()
    
    # Determine fixed column width based on maximum index length
    max_index = len(hex_str) - 1
    width = max(2, len(str(max_index)))
    
    # Build header and value rows with centered formatting
    header = "  ".join(f"{i:^{width}}" for i in range(len(hex_str)))
    values = "  ".join(f"{c:^{width}}" for c in hex_str)
    
    print("Index: ", header)
    print("Value: ", values)


def process_multiple_numbers():
    """Process multiple numbers entered by the user and highlight identical indices."""
    print("Enter multiple numbers (hex or decimal), one per line. When finished, press enter on an empty line:")
    lines = []
    while True:
        line = input()
        if line.strip() == "":
            break
        lines.append(line.strip())
    if not lines:
        print("No numbers entered.")
        return
    
    hex_list = []
    for line in lines:
        # Remove any spaces from the input
        stripped = line.replace(" ", "")
        try:
            if stripped.startswith("0x"):
                value = int(stripped, 16)
                hex_str = hex(value)[2:].upper()
            elif stripped.isdigit():
                value = int(stripped)
                hex_str = hex(value)[2:].upper()
            else:
                hex_str = stripped.upper()
        except ValueError:
            print(f"Invalid input: {line}")
            return
        hex_list.append(hex_str)
    
    # Determine the maximum length among the hex strings
    max_len = max(len(s) for s in hex_list)
    
    # Pad each hex string with leading zeros to ensure they all have the same length
    padded_hex = [s.zfill(max_len) for s in hex_list]
    
    # Convert each padded hex string into a list of characters (for column-wise comparison)
    rows = [list(s) for s in padded_hex]
    width = max(2, len(str(max_len - 1)))
    
    # Determine which columns have identical digits across all rows
    common_columns = []
    for i in range(max_len):
        digits = {row[i] for row in rows}
        common_columns.append(len(digits) == 1)
    
    # ANSI color codes for highlighting (green) without extra dependencies
    HIGHLIGHT = "\033[92m"
    RESET = "\033[0m"
    
    # Print header row with indices, highlighting columns that are identical
    header_strs = []
    for i in range(max_len):
        col_str = f"{i:^{width}}"
        if common_columns[i]:
            col_str = f"{HIGHLIGHT}{col_str}{RESET}"
        header_strs.append(col_str)
    header_line = "  ".join(header_strs)
    print("Index: ", header_line)
    
    # Print each row's hex digits, highlighting the identical columns
    for row in rows:
        row_strs = []
        for i, digit in enumerate(row):
            cell = f"{digit:^{width}}"
            if common_columns[i]:
                cell = f"{HIGHLIGHT}{cell}{RESET}"
            row_strs.append(cell)
        print("Value: ", "  ".join(row_strs))


def main():
    mode = input("Enter '1' for a single number or 'm' for multiple numbers: ").strip().lower()
    if mode == '1':
        user_input = input("Enter a number (hex or decimal): ").strip().replace(" ", "")
        try:
            if user_input.startswith("0x"):
                value = int(user_input, 16)
            elif user_input.isdigit():
                value = int(user_input)
            else:
                value = user_input  # Assume it's already a hex string
            format_number(value)
        except ValueError:
            print("Invalid input. Please enter a valid number.")
    elif mode == 'm':
        process_multiple_numbers()
    else:
        print("Invalid mode. Please enter '1' or 'm'.")


if __name__ == "__main__":
    main()
