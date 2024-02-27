import shutil
import os
import time
import filecmp
import threading

origem = input("Origin: ")
destino = input("Fate: ")

def menu():
    print("Menu:")
    print("1. Copy Folder")
    print("2. Update Folder")
    print("3. Delete File")
    print("4. Sair")

def main_menu():
    while True:
        menu()
        escolha = input("Digite o número da opção desejada: ")

        if escolha == "1":
            copy_folder()
        elif escolha == "2":
            update_folder(origem, destino)
        elif escolha == "3":
            delete_fic()
        elif escolha == "4":
            print("Saindo...")
            break
        else:
            print("Opção inválida. Por favor, escolha uma opção válida.")
    
def copy_folder(): #Copies the files that are in the source folder to the destination folder
    for file_name in os.listdir(origem):
        caminho_origem = os.path.join(origem, file_name)
        caminho_destino = os.path.join(destino, file_name)
        shutil.copy(caminho_origem, caminho_destino)
        
        logs = open("C:/Users/smart/OneDrive/Documentos/origem/Logs.txt", "a")
        logs.write("Files copied successfully."+ time.ctime(time.time())+"\n")
        logs.close()
        print("Files copied successfully.")


    
def update_folder(origem, destino): #Check if the files in the source folder have changed or if there are different files, if there are different files in the destination folder ask if you want to delete
    dcmp = filecmp.dircmp(origem, destino)
    if len(dcmp.diff_files) == 0 and len(dcmp.left_only) == 0 and len(dcmp.right_only) == 0:
        print("The two folders are identical.")
    else:
        print("Folders differ:")
        if len(dcmp.diff_files) > 0:
            print("Different files:")
            for df in dcmp.diff_files:
                print(df)
        if len(dcmp.left_only) > 0:
            print("Files only in:", origem + ":")
            for lo in dcmp.left_only:
                print(lo)
                # Copiar arquivos ausentes da pasta 2 para a pasta 1
                src_file = os.path.join(origem, lo)
                dst_file = os.path.join(destino, lo)
                shutil.copy2(src_file, dst_file)
                print(f"Arquivo {lo} copiado de {origem} para {destino}.")
        if len(dcmp.right_only) > 0:
            print("Files only in:", destino + ":")
            for ro in dcmp.right_only:
                print(ro)
                file_del = destino+ "/" + ro 
                apag = input("# Do you delete the file? y/n# - ")
                if apag == "y":
                    os.unlink(file_del)
                    print(f"File {ro} deleted successfully!")
                    logs = open("C:/Users/smart/OneDrive/Documentos/origem/Logs.txt", "a")
                    logs.write(f"File {ro} deleted successfully."+ time.ctime(time.time())+"\n")
                    logs.close()
                else:
                    print("Loading menu!")
                    main_menu()

def delete_fic():#It asks the user in which of the inserted folders it wants to delete a file, it gives you the option to choose between the source folder and the destination folder, then it asks you to say which file (with extension) you want to delete.
    direc = input("What folder is the file in? O - origin | d - fate - ")
    file = input("Enter the file to delete: (with extension) - ")
    
    apag = input("# Do you delete the file? y/n# - ")
    if apag == "y":
        if direc == "o" or direc == "O":
            file_ori = origem + "/" + file
            os.unlink(file_ori)
            print(f"File {file_ori} deleted successfully!")
            logs = open("C:/Users/smart/OneDrive/Documentos/origem/Logs.txt", "a")
            logs.write(f"File {file_ori} deleted successfully."+ time.ctime(time.time())+"\n")
            logs.close()
        elif direc == "d" or direc == "D":
            file_deS = destino+ "/" + file
            os.unlink(file_deS)
    else:
        print("Loading menu!")
        main_menu()




# def temporizador(time_time, update_folder):
#    timer = threading.Timer(time_time, update_folder)
#    timer.start()

#time_time = 300

#temporizador(time_time, update_folder)

if __name__ == "__main__":
    main_menu()