# OklandCrime
def createdataset(file):создание датасета 
    try:
        dataseti=dict()
        time=dict()
        location=dict()
        with open(file,'r') as f:
            file_line=f.readline()
            if not file_line:
                return dataseti
            header = file_line.rstrip().split(",")
            file_line=f.readline()
            file_line1 = file_line[:20]
            while file_line:
                [Agency,Create_time,location,Area_id,Beat,priority,Type_id,Type_desc,Event_number,Closet_time]=[element.strip() for     element in file_line1.rstrip().split(",")]
            if location not in dataseti:
                dataseti[location]=dict()
            if Create_time not in dataseti[location]:
                dataseti[Create_time]=dict()
                dataseti.update({
                    Create_time:{
                        "Event number":Event_number,
                        "priority":priority,
                        "Type_id":Type_id,
                        "Type_desc":Type_desc,
                        "Closet_time":Closet_time
                         },
                    location:{
                        "Area id":Area_id,
                        "Beat": Beat,
                        "Agency":Agency
                        }
                })
                file_line=f.readline()
        return dataseti
    except IOError as e:
        print("I/O error({0}): {1}".format(e.errno, e.strerror))
        return dict()

