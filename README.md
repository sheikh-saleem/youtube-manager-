# youtube-manager-
import json

def load_data():
    try:
        with open("youtube.txt","r") as file:
            test= json.load(file)
            # print(type(test))
            return test
    except FileNotFoundError :
        return []

def save_data_helper(videos):
    with open("youtube.txt","w") as file:
        json.dump(videos,file)

def list_all_videos(videos):
    print("\n")
    print("*" * 70)
    for index,video in enumerate(videos,start=1) : 
        print(f"{index}.{video['name']},duration:{video['time']} ")
    print("\n")
    print("*" * 70)

def add_video(videos):
    name=input("enter video name")
    time=input("enter video time")
    videos.append({'name': name, 'time':time})
    save_data_helper(videos)


def update_video(videos):
    list_all_videos(videos)
    index=int(input("enter a number to update"))
    if 1<=index <= len(videos):
        name=input("enter the video name")
        time=input("enter the video time")
        videos[index-1 ]={'name':name,'time':time}
        save_data_helper(videos)
    else:
        print("invalid edit select")

def delete_video(videos):
    list_all_videos(videos)
    index=int(input("enter the video number to be delete"))
    if 1 <= index <= len(videos):
        del videos [index-1]
        save_data_helper(videos)
    else:
        print("invalid video select")
def main ():
    videos=load_data()
    while True:
        print("\n youtube manager | choose an option")
        print("1.list all youtube videos")
        print("2.add a youtube videos")
        print("3.update all youtube videos deatils")
        print("4.delet all youtube videos ")
        print("5.exit a app ")
        file=input("enter your choise...")
        # print(videos) 

        match file:
            case '1':
                list_all_videos(videos)
            case '2':
                add_video(videos)
            case '3':
                update_video(videos)
            case '4':
                delete_video(videos)
            case '5':
                break
            case _:
                print("invalid choice")
if __name__ == "__main__":
    main()
