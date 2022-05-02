# prototype.Promise.methods
Promis.all/Promise.any/Promise.allsetteled/Promise.race


//Promise.all
const promise1 = new Promise((res) => {
  setTimeout(() => {
    res("1st promise resolved");
  }, 1000);
});
const promise2 = Promise.resolve("2nd promise resolve");
const promise3 = Promise.reject("3rd promise rejected");

Promise.myAny = (iterator) => {
  const storePromise = [];
  let count = 0;
  return new Promise((resolve, reject) => {
    iterator.forEach((data,index) => {
        Promise.resolve(data).then((value) => {
          count++;
          storePromise[index] = value;
          if (count === iterator.length) {
            resolve(storePromise);
          }
        })
        .catch((err) => reject(err));
    });
  });
};

Promise.myAny([promise1,promise2,promise3]).then((value)=>console.log(value)
).catch((err)=>console.error(err))
