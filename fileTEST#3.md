import os

def get_file_info(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        lines = file.readlines()
    return file_path, len(lines), lines

def merge_files(file_paths, output_file):
    file_info_list = [get_file_info(file_path) for file_path in file_paths]
    file_info_list.sort(key=lambda x: x[1])  # Сортировка по количеству строк

    with open(output_file, 'w', encoding='utf-8') as out_file:
        for file_path, line_count, lines in file_info_list:
            out_file.write(f"{os.path.basename(file_path)}\n")
            out_file.write(f"{line_count}\n")
            out_file.writelines(lines)
            out_file.write("\n")  # Добавляем пустую строку между файлами

# Пример использования
file_paths = ['1.txt', '2.txt', '3.txt']
output_file = 'result.txt'

merge_files(file_paths, output_file)
print(f"Файлы объединены в {output_file}")