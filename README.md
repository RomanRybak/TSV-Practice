# TSV-Practice

# Hello, this program adds another column to the table and displays the mean frequency in each row 

import csv, sys
#first creating a class function
#then converting tsv to csv file for easier use
def tsv_practice():
    try: #seeing if the file exist in a computer
        with open('freqs.tsv','r') as file_:
            oreo = csv.reader(file_, delimiter='\t')
            file_contents = [line for line in oreo]
    
        with open('testing.csv','w') as lfile:
            cw = csv.writer(lfile, quotechar='', quoting=csv.QUOTE_NONE, escapechar='\\')
            cw.writerows(file_contents)
            lfile.close()
    except:
        print("file freqs.tsv does not exist")
        sys.exit()

    #now converting csv file back to tsv, even though it would look much prettier staying csv
    with open('testing.csv', 'r') as csvinput:
        with open("freqs-mean.tsv", "w") as csvoutput:
            csv_reader = csv.reader(csvinput, delimiter=",")
            csv_writer = csv.writer(csvoutput, delimiter=",")
            #next_line = next(reader, None)
            Sum = 0
            #row=[]
            for row in csv_reader:
                Sum = sum((float(i) if i else Sum) for i in row[1:])
                row.append(Sum/len(row[1:]) if Sum else Sum)
                csv_writer.writerow(row)
                
tsv_practice()
