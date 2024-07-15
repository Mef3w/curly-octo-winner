import threading

from logger.components.connection_logger import ConnectionLoggingMetaclass


class Connection(metaclass=ConnectionLoggingMetaclass):
    def __init__(self, socket):
        self.socket = socket
        self.address = socket.getpeername()
        self.thread = threading.Thread(target=self.__start_connection)
        self.thread.start()

    def __start_connection(self):
        try:
            return self.__handle_connection()
        except Exception as e:
            self.socket.close()
            return e

    def __handle_connection(self):
            message = self.socket.recv(1024).decode('utf-8')
            self.__handle_message(message)

    def __handle_message(self, message):
        if message:
            print(f"Message from {self.address}: {message}")
        return self.__handle_connection()




    def send_message(self, message):
        # message = Message(self.socket, message)
        self.socket.send(message.encode('utf-8'))
