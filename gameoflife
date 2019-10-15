from tkinter import Tk, Canvas, Button, Frame, BOTH, NORMAL, HIDDEN


def adres(ii, jj):
    if ii < 0 or jj < 0 or ii >= field_height or jj >= field_width:
        return len(cell_matrix) - 1
    else:
        return ii * (int(win_width / cell_size)) + jj


def draw_a(e):
    ii = (e.y - 3) / cell_size
    jj = (e.x - 3) / cell_size
    canvas.itemconfig(cell_matrix[adres(ii, jj)], state=NORMAL, tags='vis')


def newcells():
    for i in range(field_height):
        for j in range(field_width):
            k = 0
            for m in range(-1, 2):
                for n in range(-1, 2):
                    if (canvas.gettags(cell_matrix[adres(i + m, j + n)])[0] == 'vis' and (
                            m != 0 or n != 0)):
                        k += 1
            current_tag = canvas.gettags(cell_matrix[adres(i, j)])[0]
            if k == 3:
                canvas.itemconfig(cell_matrix[adres(i, j)], tags=(current_tag, 'to_vis'))
            if k <= 1 or k >= 4:
                canvas.itemconfig(cell_matrix[adres(i, j)], tags=(current_tag, 'to_hid'))
            if k == 2 and canvas.gettags(cell_matrix[adres(i, j)])[0] == 'vis':
                canvas.itemconfig(cell_matrix[adres(i, j)], tags=(current_tag, 'to_vis'))


def newpicture():
    for i in range(field_height):
        for j in range(field_width):
            if canvas.gettags(cell_matrix[adres(i, j)])[1] == 'to_hid':
                canvas.itemconfig(cell_matrix[adres(i, j)], state=HIDDEN, tags=('hid', '0'))
            if canvas.gettags(cell_matrix[adres(i, j)])[1] == 'to_vis':
                canvas.itemconfig(cell_matrix[adres(i, j)], state=NORMAL, tags=('vis', '0'))


def evolution():
    newcells()
    newpicture()


root = Tk()
root.title('Игра в жизнь')
win_width = 1000
win_height = 600
config_string = "{0}x{1}".format(win_width, win_height + 32)
root.geometry(config_string)
fill_color = "black"
root.geometry(config_string)
cell_size = 20
canvas = Canvas(root, height=win_height)
canvas.pack(fill=BOTH)

field_height = int(win_height / cell_size)
field_width = int(win_width / cell_size)

cell_matrix = []
for i in range(field_height):
    for j in range(field_width):
        square = canvas.create_rectangle(2 + cell_size * j, 2 + cell_size * i, cell_size + cell_size * j - 2,
                                         cell_size + cell_size * i - 2, fill=fill_color)
        canvas.itemconfig(square, state=HIDDEN, tags=('hid', '0'))
        cell_matrix.append(square)
fict_square = canvas.create_rectangle(0, 0, 0, 0, state=HIDDEN, tags=('hid', '0'))
cell_matrix.append(fict_square)

canvas.itemconfig(cell_matrix[adres(12, 23)], state=NORMAL, tags='vis')
canvas.itemconfig(cell_matrix[adres(14, 24)], state=NORMAL, tags='vis')
canvas.itemconfig(cell_matrix[adres(13, 24)], state=NORMAL, tags='vis')
canvas.itemconfig(cell_matrix[adres(13, 23)], state=NORMAL, tags='vis')
canvas.itemconfig(cell_matrix[adres(13, 22)], state=NORMAL, tags='vis')
canvas.itemconfig(cell_matrix[adres(14, 22)], state=NORMAL, tags='vis')

frame = Frame(root)
btn = Button(frame, text='Следующее поколение', command=evolution)
btn.pack()
frame.pack(side='bottom')

canvas.bind('<B1-Motion>', draw_a)
canvas.bind('<ButtonPress>', draw_a)

root.mainloop()
