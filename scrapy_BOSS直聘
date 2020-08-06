from requests import get
import parsel
#import clear_cookie
from time import sleep

for page in range(1,1000):
    print('\n##########正在下载第{}页数据##########\n'.format(page))
    base_url = 'https://www.zhipin.com/c100010000-p100109/?page={}&ka=page-{}'.format(page,page)
    if page>1:
        sleep(5)

    cookie = 'Hm_lvt_194df3105ad7148dcf2b98a91b5e727a=1596689319,1596706170; lastCity=100010000; __g=-; __zp_stoken__=a22daJB4DI1lsZkxcNEotc3AEMXhEbHRqFFdAYwB7JnIMWydyTWshf2pXaGIpFndlLUcoPGVnDFJ0PTAYFwhsHnJqKx0nInloej8bZVR9OyoNIBtUZ1xOB31HTgcZKwkub35tQxcGDVg2eT4%3D; Hm_lpvt_194df3105ad7148dcf2b98a91b5e727a=1596706456; __zp_sseed__=+ESIwp4DFQO7vkpLz5T9FtTBTD9zO5XO5H3GNSZMuTc=; __zp_sname__=cfe88225; __zp_sts__=1596706745034; __c=1596706172; __l=l=%2Fwww.zhipin.com%2Fc100010000-p100109%2F%3Fpage%3D10%26ka%3Dpage-10&r=&g=; __a=84984979.1596689321.1596689321.1596706172.20.2.12.20'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36',
        'cookie': cookie,
    }

    html_data = get(url=base_url,headers=headers).text


    selector = parsel.Selector(html_data)
    result_list = selector.css("#main > div > div.job-list > ul > li")
    for sel in result_list:
        Job_benefits = sel.css("div > div.info-append.clearfix > div.info-desc ::text").extract_first() #工作福利

        job_name = sel.css("div > div.info-primary > div.primary-wrapper > div > div.job-title > span.job-name > a ::text").extract_first()

        Working_data_1 = sel.css("div > div.info-append.clearfix > div.tags > span:nth-child(1) ::text").extract_first() #工作数据_1
        Working_data_2 = sel.css("div > div.info-append.clearfix > div.tags > span:nth-child(2) ::text").extract_first()  # 工作数据_2
        Working_data_3 = sel.css("div > div.info-append.clearfix > div.tags > span:nth-child(3) ::text").extract_first()  # 工作数据_3
        Working_data_4 = sel.css("div > div.info-append.clearfix > div.tags > span:nth-child(4) ::text").extract_first()  # 工作数据4
        Working_data_5 = sel.css("div > div.info-append.clearfix > div.tags > span:nth-child(5) ::text").extract_first()  # 工作数据_5
        Working_data = str(str(Working_data_1) + ' ' + str(Working_data_2) + ' ' + str(Working_data_3) + ' ' + str(Working_data_4) + ' ' + str(Working_data_5))

        employer = sel.css("div > div.info-primary > div.info-company > div > h3 > a ::text").extract_first()


        work_place = sel.css("div > div.info-primary > div.primary-wrapper > div > div.job-title > span.job-area-wrapper > span ::text").extract_first() #工作地点

        work_money = sel.css("div > div.info-primary > div.primary-wrapper > div > div.job-limit.clearfix > span ::text").extract_first() #工资

        Job_requirements_1 = sel.xpath('./div/div[1]/div[1]/div/div[2]/p/text()[1]').extract_first() #工作要求_1
        Job_requirements_2 = sel.xpath('./div/div[1]/div[1]/div/div[2]/p/text()[2]').extract_first() #工作要求_2
        Job_requirements = str(Job_requirements_1 + ' ' + Job_requirements_2)

        #print(Job_requirements)




        job_data = {
            '工作': job_name,
            '工作要求': Job_requirements,
            '工资': work_money,
            '雇主': employer,
            '工作数据': Working_data,
            '工作地点': work_place,
            '工作福利': Job_benefits,

        }



        with open('job_data.csv',mode='a+',encoding='utf-8') as f:
            job_data_write = str(job_data)
            f.write(job_data_write+'\n')
            print('保存完成:',job_data)
