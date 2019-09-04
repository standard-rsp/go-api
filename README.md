# ogs-go
Return a well-structured data format for golang api

#### RspBase(code int, message BaseMessage):
 only return code and message
 
```go
import "github.com/ogsapi/ogs-go"

func Example() interface{} {
	return ogs.RspBase(ogs.StatusTokenExpired, ogs.ErrorMessage("Token Expired！"))
}

/**
{
  message: {
    message: "Token Expired！",
    type: "error"
  },
  code: 10002
}
 */
```

#### RspBaseWithData(code int, message BaseMessage, data interface{}):
 return code, message and data
 
```go
func Example() interface{} {
	data := map[string]interface{}{"test": "test"}
	return ogs.RspBaseWithData(ogs.StatusOK, ogs.BlankMessage(), data)
}

/**
{
    "code": 0,
    "message": {
        "message": "",
        "type": ""
    },
    "data": {
        "test": "test"
    }
}
 */
```

#### RspBaseWithPaginate(code int, message BaseMessage, data interface{}, basePaginate BasePaginate):
 return code, message, data and Paginate
 
```go
func Example() interface{} {
	var users []User
    count := 0
    db.Find(&users).Count(&count)

    return ogs.RspBaseWithPaginate(
        ogs.StatusOK,
        ogs.BlankMessage(),
        users,
        ogs.NewPaginate(1, count, 10))
}

/**
{
    "code": 0,
    "message": {
        "message": "",
        "type": ""
    },
    "data": [
        {
            "email": "admin@test.com",
            "nickname": "admin"
        },
        {
            "email": "test@test.com",
            "nickname": "test"
        }
    ],
    "paginate": {
        "current_page": 1,
        "total_pages": 1,
        "total_count": 3,
        "per_page": 10
    }
}
 */
```

Response with OK(code is 0)
#### RspOK(message BaseMessage)
#### RspOKWithData(message BaseMessage, data interface{})
#### RspOKWithPaginate(message BaseMessage, data interface{}, basePaginate BasePaginate)



default code:

    StatusOK = 0
    
    // authorization
    StatusUnauthorized  = 10001
    StatusTokenExpired  = 10002
    StatusInvalidToken  = 10003
    StatusUserNotFound  = 10004
    StatusErrorPassword = 10005

    // system and resources
    StatusSystemError     = 20001
    StatusResourceExpired = 20002

    // crud
    StatusCreateFailed       = 30001
    StatusUpdateFailed       = 30002
    StatusDestroyFailed      = 30003
    StatusBatchCreateFailed  = 30004
    StatusBatchUpdateFailed  = 30005
    StatusBatchDestroyFailed = 30006
