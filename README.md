# to handle the json file:
import json 
# to handle times and dates:
import datetime

# setting a global file name veriable
file_name = 'task.json'

# this function is checking if the file path doesnt exists or empty and handles it. 
def file_check():
    global file_name # bringing our global var
    tasks = [] 
    if os.path.exists(file_name) and os.path.getsize(file_name) > 0:
        with open(file_name, 'r', encoding='utf-8') as task_file:
            try:
                tasks = json.load(task_file)
            except json.JSONDecodeError:
                tasks = []
    return tasks

# this function is adding a new task to the json file with a param of the task description
def AddTask(description):
    global file_name
    tasks = file_check()
    if tasks:
        new_id = max(task['ID'] for task in tasks) + 1
    else:
        new_id = 1    
    
    status = 'todo'
    now = datetime.datetime.now().isoformat()
    task = {'ID' : new_id, 
    'Description' : description,
    'Status' : status,
    'Created_at': now,
    'Updated_at' : now
    }
    
    
    tasks.append(task)
                                
    with open(file_name, 'w') as task_file:
        json.dump(tasks, task_file, indent=4)
                    
# this function is updating the task status                  
def updateTask(id, status):
    global file_name
    tasks = file_check()
            
    for task in tasks:
        if task['ID'] == id:
            task['Status'] = status
            task['Updated_at'] = datetime.datetime.now().isoformat()
        else: 
             pass   
    with opn(file_name, 'w') as task_file:
        json.dump(tasks, task_file, indent=4)
            
# this function is deleting a wanted task by its id           
def delTask(id):
    tasks = file_check()
    tasks = [task for task in tasks if task['ID'] != id]
    with open(file_name, 'w') as task_file:
            json.dump(tasks, task_file, indent=4)
            
# this function will print to the console all the tasks in the json          
def getAllTasks():
    tasks = file_check()
    print(tasks)
    
# this function will print to the console all the tasks with the wanted status    
def getTaskbystatus(status):
    
        tasks = file_check()
        filtered_list = []
        for task in tasks:
            if task['Status'] == status:
                filtered_list.append(task)
            else:
                pass
        print(filtered_list)

# try..          
AddTask('Learn python')
getAllTasks()
AddTask('Watch tv series')
updateTask(1, 'in-progress')
getTaskbystatus('in-progress')
getAllTasks()
updateTask(2, 'done')
getTaskbystatus('done')    

https://roadmap.sh/projects/task-tracker

    

            
            

    
    
    
        
