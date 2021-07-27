# new

print("Игра крестики-нолики. Добро пожаловать!")
print("-" * 39)
print("Форма ввода: координаты х, у")
print("х - номер строки")
print("у - номер столбца")

# Создаём поле
playing_table = [[" "] * 3 for i in range(3)]
playing_table 

# Выводим поле на экран
def board(): # Функция вывода на экран
    print()
    print("   | 0 | 1 | 2 |")
    print("-" * 16)
    for i, row in enumerate(playing_table):
       row_str = f" {i} | {' | '.join(row)} | "
       print(row_str)
       print("-" * 16)
    print()    
   
board()

# Ввод координат пользователем, и провека этих координат на првавильность ввода

def location():
    while True:
        cords = input("Введите координаты:   ").split()
        
        if len(cords) != 2 :
            print("Введите две координаты !")
            continue
       
        x, y = cords

        if not(x.isdigit()) or not(y.isdigit()):
            print("Введите числа!")
            continue

        x, y = int(x), int(y)

        if 0 > x or x > 2 or 0 > y or y > 2 :
            print("Координаты вне диапазона!")
            continue

        if playing_table[x][y] != " ":
            print("Клетка занята!")
            continue
        return x, y           
     
location()

# Запись выигрышных комбанаций
def check_win():
    win_cord = [((0, 0), (0, 1), (0, 2)), ((1, 0), (1, 1), (1, 2)), ((2, 0), (2, 1), (2, 2)),
                ((0, 2), (1, 1), (2, 0)), ((0, 0), (1, 1), (2, 2)), ((0, 0), (1, 0), (2, 0)),
                ((0, 1), (1, 1), (2, 1)), ((0, 2), (1, 2), (2, 2))]
    for cord in win_cord:
        a = cord[0]
        b = cord[1]
        c = cord[2]

        if playing_table[a[0]][a[1]] == playing_table[b[0]][b[1]] == playing_table[c[0]][c[1]] != " ":
            print(f"Выиграл {playing_table[a[0]][a[1]]}!")                
            return True
    return False

num = 0
while True:
    num += 1
    board()
    if num % 2 == 1:
        print("Ходит крестик.")
    else:
        print("Ходит нолик.")
    
    x, y = location()

    if num % 2 == 1:
        playing_table[x][y] = "X"
    else:
        playing_table[x][y] = "0"

    if check_win():
        break    
    
    if num == 9:
        print("Ничья!")
        break
