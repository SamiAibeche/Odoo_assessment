# Odoo_assessment
```py
## Check for if closed tag
def IsClosingTag(tag):
    if len(tag) > 2:
        return tag[1] == '/'


## Find a tag in the string given
def FindTag(strParam, start):
    openedTag = strParam.find('<', start)
    if openedTag != -1:  # found opening bracket
        closedTag = strParam.find('>', openedTag + 1)
        if closedTag != -1:  # found whole tag
            tag = strParam[openedTag:closedTag + 1]
            return (tag, closedTag + 1)
    else:
        return (None, -1)


def CheckDom(strParam):
    open_tags = []
    i = 0
    if strParam != '': #check for emptu string
        while i < len(strParam):

            tag, i = FindTag(strParam, i)  #get a list of result
            if tag != None:
                if IsClosingTag(tag):
                    if len(open_tags) != 0:
                        if open_tags[-1][1: -1] == tag[2:-1]:
                           open_tags.pop()
                else:
                    open_tags.append(tag)
            else:
                return "false"
    else:
        return "false"

    if len(open_tags) == 0:
        return "true"
    elif len(open_tags) == 1:
        return open_tags[0]
    else:
        return "false"

## Unit Tests
print(CheckDom("<b></b>"))
print(CheckDom(""))
print(CheckDom("sdfdsf>"))
print(CheckDom("<b></b>"))
print(CheckDom("<b><p><p></p></b>"))
print(CheckDom("<b><p><p></p></p></b>"))

```
